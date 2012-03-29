Mozmill CI
==========

With the Mozmill CI project we aim to get a fully automated testing cycle implemented for testing Firefox in the Mozilla QA compartment. Therefore the [Mozilla Pulse](http://pulse.mozilla.org/) message broker and [Jenkins](http://jenkins-ci.org/) are used.

Setup
-----
Before you can start the system the following commands have to be performed:

    git clone git://github.com/whimboo/mozmill-ci.git
    cd mozmill-ci
    ./setup/configure.sh

Startup
-------
The two components (Pulse consumer and Jenkins master) have to be started separately in two different terminals. As first step we have to setup the Jenkins master:

    ./start.sh

Once Jenkins has been fully started, open `http://localhost:8080/` via your web browser. Open the `+admin` view and execute all of the listed jobs once.

Now you can start the Pulse consumer which pushes requests for jobs through the Jenkins API to the master:

    source jenkins-env/bin/activate
    ./pulse.py config/example_daily.cfg

Please keep in mind that you should create your own configuration file before you start the consumer and setup the wanted builds appropriately.

Adding new Nodes
----------------
To add Jenkins slaves to your master you have to create new nodes. You can use the `windows_xp_32_01` node settings as a template. Once done the nodes have to be connected to the master. Therefore [install Java](www.java.com/download/) on the node and open the appropriate node page from the nodes web browser like:

    http://IP:8080/computer/windows_xp_32_01/

Now click the `Launch` button and the node should automatically connect to the master. It will be used once a job for this type of platform has been requested by the Pulse consumer.