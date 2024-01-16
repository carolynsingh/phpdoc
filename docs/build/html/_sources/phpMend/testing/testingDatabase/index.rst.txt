SETTING UP TESTING DATABASE
=================================

**Step 1 :**

The first step is to create a database.
This database should be a clone of your real database, which is used by the application but should not contain any data inside the tables.

.. image:: images/img_2.png

**Step 2 :**

In .env file add the following keys :

.. code-block::

   DB_TEST_HOST=127.0.0.1
   DB_TEST_PORT=3306
   DB_TEST_DATABASE=testdb
   DB_TEST_USERNAME=root
   DB_TEST_PASSWORD=Qwerty@321

.. note::

   Change the "Port" , "Database name" and "Password" according to your credentials.

**Step 3 :**

Alter APP_ENV key in .env file :

.. code-block::

   APP_ENV=testing

**Step 4 :**

Put the below code in config/database.php :

.. code-block:: php

   'testing' => [
            'driver' => 'mysql',
            'url' => env('DATABASE_URL'),
            'host' => env('DB_TEST_HOST', '127.0.0.1'),
            'port' => env('DB_TEST_PORT', '3306'),
            'database' => env('DB_TEST_DATABASE', 'forge'),
            'username' => env('DB_TEST_USERNAME', 'forge'),
            'password' => env('DB_TEST_PASSWORD', ''),
            'unix_socket' => env('DB_SOCKET', ''),
            'charset' => 'utf8mb4',
            'collation' => 'utf8mb4_unicode_ci',
            'prefix' => '',
            'prefix_indexes' => true,
            'strict' => true,
            'engine' => null
        ],

.. note::

   Put the above code just after mysql array.

**Step 5 :**

Add the below code in phpunit.xml file :

.. code-block::

   <env name="DB_CONNECTION" value="testing"/>

.. image:: images/img.png

**Step 6 :**

Run the command to migrate tables in the testing database :

.. code-block::

   php artisan migrate:fresh --database=testing --seed