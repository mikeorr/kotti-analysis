Tables
++++++

Document-related tables
=======================

.. code-block:: sql

    CREATE TABLE nodes (
        id INTEGER NOT NULL, 
        type VARCHAR(30) NOT NULL, 
        parent_id INTEGER, 
        position INTEGER, 
        _acl TEXT, 
        name VARCHAR(50) NOT NULL, 
        title VARCHAR(100), 
        annotations TEXT, 
        PRIMARY KEY (id), 
        UNIQUE (parent_id, name), 
        FOREIGN KEY(parent_id) REFERENCES nodes (id)
    );

    CREATE TABLE contents (
        id INTEGER NOT NULL, 
        default_view VARCHAR(50), 
        description TEXT, 
        language VARCHAR(10), 
        owner VARCHAR(100), 
        state VARCHAR(50), 
        creation_date DATETIME, 
        modification_date DATETIME, 
        in_navigation BOOLEAN, 
        PRIMARY KEY (id), 
        FOREIGN KEY(id) REFERENCES nodes (id), 
        CHECK (in_navigation IN (0, 1))
    );

    CREATE TABLE documents (
        id INTEGER NOT NULL, 
        body TEXT, 
        mime_type VARCHAR(30), 
        PRIMARY KEY (id), 
        FOREIGN KEY(id) REFERENCES contents (id)
    );

Special content type tables
===========================

.. code-block:: sql

    CREATE TABLE files (
        id INTEGER NOT NULL, 
        data BLOB, 
        filename VARCHAR(100), 
        mimetype VARCHAR(100), 
        size INTEGER, 
        PRIMARY KEY (id), 
        FOREIGN KEY(id) REFERENCES contents (id)
    );

    CREATE TABLE images (
        id INTEGER NOT NULL, 
        PRIMARY KEY (id), 
        FOREIGN KEY(id) REFERENCES files (id)
    );

Tag-related tables
==================

.. code-block:: sql

    CREATE TABLE tags (
        id INTEGER NOT NULL, 
        title VARCHAR(100) NOT NULL, 
        PRIMARY KEY (id), 
        UNIQUE (title)
    );
    CREATE TABLE tags_to_contents (
        tag_id INTEGER NOT NULL, 
        content_id INTEGER NOT NULL, 
        position INTEGER NOT NULL, 
        PRIMARY KEY (tag_id, content_id), 
        FOREIGN KEY(tag_id) REFERENCES tags (id), 
        FOREIGN KEY(content_id) REFERENCES contents (id)
    );

User and group-related tables
=============================

.. code-block:: sql

    CREATE TABLE local_groups (
        id INTEGER NOT NULL, 
        node_id INTEGER, 
        principal_name VARCHAR(100), 
        group_name VARCHAR(100), 
        PRIMARY KEY (id), 
        UNIQUE (node_id, principal_name, group_name), 
        FOREIGN KEY(node_id) REFERENCES nodes (id)
    );

    CREATE TABLE principals (
        id INTEGER NOT NULL, 
        name VARCHAR(100), 
        password VARCHAR(100), 
        active BOOLEAN, 
        confirm_token VARCHAR(100), 
        title VARCHAR(100) NOT NULL, 
        email VARCHAR(100), 
        groups TEXT NOT NULL, 
        creation_date DATETIME NOT NULL, 
        last_login_date DATETIME, 
        PRIMARY KEY (id), 
        UNIQUE (name), 
        CHECK (active IN (0, 1)), 
        UNIQUE (email)
    );

Database migration tables
=========================

.. code-block:: sql

    CREATE TABLE kotti_alembic_version (
        version_num VARCHAR(32) NOT NULL
    );

