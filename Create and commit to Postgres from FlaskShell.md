### How to run commands with PostgresSQL from Flask Shell

#### 1. Enter a Flask shell
    $ flask shell

#### 2. Import the database
    >>> from app import db

#### 3. Create DB (if it doesn't exist)
    >>> db.create_all()

#### 4. Insert a new row into Table
    admin_role = Role(name='Admin')
Note: `Role` is the name of the class in code (not the table name,
which is `roles` and was specified in the `__tablename__` attribute)

#### 5. Commit the changes
    >>> db.session.add(admin_role)
    >>> db.session.commit()


```bash 


