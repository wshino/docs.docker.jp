.. -*- coding: utf-8 -*-
.. URL: https://docs.docker.com/engine/reference/commandline/volume_create/
.. SOURCE: https://github.com/docker/docker/blob/master/docs/reference/commandline/volume_create.md
   doc version: 1.10
      https://github.com/docker/docker/commits/master/docs/reference/commandline/volume_create.md
.. check date: 2016/02/25
.. Commits on Feb 10, 2016 910ea8adf6c2c94fdb3748893e5b1e51a6b8c431
.. -------------------------------------------------------------------

.. volume create

=======================================
volume create
=======================================

.. sidebar:: 目次

   .. contents:: 
       :depth: 3
       :local:

.. code-block:: bash

   Usage: docker volume create [OPTIONS]
   
   Create a volume
   
     -d, --driver=local    Specify volume driver name
     --help                Print usage
     --name=               Specify volume name
     -o, --opt=map[]       Set driver specific options

.. Creates a new volume that containers can consume and store data in. If a name is not specified, Docker generates a random name. You create a volume and then configure the container to use it, for example:

コンテナが利用し、データを保管するための新しいボリュームを作成します。名前を指定しなければ、 Docker はランダムな名称を生成します。ボリュームを作成し、コンテナが使えるようにするには、次の例のように実行します。

.. code-block:: bash

   $ docker volume create --name hello
   hello
   
   $ docker run -d -v hello:/world busybox ls /world

.. The mount is created inside the container’s /world directory. Docker does not support relative paths for mount points inside the container.

これはコンテナ内の ``/world`` ディレクトリにマウントが作成されます。Docker はコンテナ内のマウントポイントに、相対パスの指定をサポートしません。

.. Multiple containers can use the same volume in the same time period. This is useful if two containers need access to shared data. For example, if one container writes and the other reads the data.

複数のコンテナが同時に同じボリュームを利用できます。２つのコンテナが共有データにアクセスする場合に便利です。例えば、一方のコンテナがデータを書き込み、もう一方がデータを読み込めます。

.. Volume names must be unique among drivers. This means you cannot use the same volume name with two different drivers. If you attempt this docker returns an error:

ボリューム名はドライバ間でユニークである必要があります。つまり２つの異なったドライバで、同じボリューム名を使うことはできません。実行しようとしても、 ``docker`` はエラーを返します。

.. code-block:: bash

   A volume named  %s  already exists with the %s driver. Choose a different volume name.

.. If you specify a volume name already in use on the current driver, Docker assumes you want to re-use the existing volume and does not return an error.

現在のドライバが既に使用しているボリューム名を指定する場合は、Docker は既存のボリュームを再利用するとみなし、エラーを返しません。

.. Driver specific options

.. _volume-create-driver-specific-options:

ドライバ固有のオプション
==============================

.. Some volume drivers may take options to customize the volume creation. Use the -o or --opt flags to pass driver options:

ボリューム・ドライバによっては、ボリューム作成のカスタマイズのためにオプションが使えます。 ``-o`` か ``--opt`` フラグでドライバにオプションを渡します。

.. code-block:: bash

   $ docker volume create --driver fake --opt tardis=blue --opt timey=wimey

.. These options are passed directly to the volume driver. Options for different volume drivers may do different things (or nothing at all).

これらのオプションは各ボリューム・ドライバに直接渡されます。オプションはボリューム・ドライバごとに別々の動作をします（あるいは何もしないかもしれません）。

.. Note: The built-in local volume driver does not currently accept any options.

.. note::

   内蔵の ``local`` ボリューム・ドライバは、現時点ではオプションを受け付けません。

関連情報
==========

* :doc:`volume_inspect`
* :doc:`volume_ls`
* :doc:`volume_rm`
* :doc:`/engine/userguide/containers/dockervolumes`

.. seealso:: 

   volume create
      https://docs.docker.com/engine/reference/commandline/volume_create/
