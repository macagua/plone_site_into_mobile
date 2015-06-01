Plone site into an mobile application
=====================================

An Plone site as an apk (Android app with PhoneGap). In detail, this is a
`WebView Android <http://developer.android.com/intl/es/guide/webapps/webview.html>`_.

Requeriments
------------

- Latest `PhoneGap <http://phonegap.com/install/>`_ version installed.

- A Plone site created using `plonethemes.suite <https://github.com/plone-ve/plonethemes.suite>`_.

- You need an accessable IP or domain name. For instance, we assume that your local instance is running on a server with the IP **192.168.10.66** on Port **8081**

- The Plone id should be **Mobile**.

- Enabled the addon **zettwerk.mobile**.

- Access to Addon Configuration ``Mobile theming``, then
  set the ``Hostnames`` to apply the mobile theme as *http://192.168.10.66:8081*.

- Choose the **zettwerk.mobile** theme via tha ``Theme Name`` field and click the ``Save`` button.

Create and the app
------------------

After phonegap installation, the ``phonegap`` tool should be available in your path variable. So you can create a new Phonegap project via::

    phonegap create MyProject

The next step is to allow your app to access the plone instance. This is done by adjusting a setting in the generated **config.xml**. Open your favorite text editor and open the config.xml file, located in the **www** directory of your created project folder. Search the line **<access origin="http://127.0.0.1\*"/>** and append a new line with (change the IP if needed)::

    <access origin="http://192.168.10.66" subdomains="true" />

Save and close the file. The last required step is, to load the content from your plone instance after the app is ready. This is done by editing the default **index.js** file, located in the **www/js** directory of your Phonegap project. Find the **deviceready** handler and change it like this::

    onDeviceReady: function() {
        app.receivedEvent('deviceready');
	window.location = 'http://192.168.10.66:8081/Mobile';
    },


Run the emulator
----------------

To test your newly created app, you can use phonegap to build the app and start it in the emulator or your connected device. The setup of emulators and devices for phonegap is beyound the scope of this readme.

For example to start the emulator with an existing emulated device just type::

    phonegap run android


Example in video
----------------

- `zettwerk.mobile + zettwerk.mobiletheming + phonegap for Plone <https://www.youtube.com/watch?v=Q2ID86XkiQQ>`_
