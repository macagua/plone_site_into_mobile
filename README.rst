Plone site into an mobile application
=====================================

An Plone site as an apk (Android app with PhoneGap). In detail, this is a
`WebView Android <http://developer.android.com/intl/es/guide/webapps/webview.html>`_.

Requeriments
------------

- Latest `PhoneGap <http://phonegap.com/install/>`_ version installed.

- A Plone site created using `plonethemes.suite <https://github.com/plone-ve/plonethemes.suite>`_.

- You need an accessable IP or domain name. For instance, we assume that your local instance is running on a server with the IP **192.168.10.66** on Port **8081**


Configure Plone
---------------

- Extend your buildout to include the egg **zettwerk.mobile** and re-run buildout.

- Start your Plone instance, open the **ZMI** and create a Plone instance with id **Mobile**

- After creation, switch to the Site Setup of Plone and click the **Mobile theming** link in the **Add-on Configuration**.

- Change the field **Hostnames** to your IP and Port. For example: ``http://192.168.10.66:8081/Plone`` - now every visitor via this URL will get a different theme, than the default.

- To choose which theme, the next field **Theme Name** is used. Choose the default ``zettwerk.mobile theme``.

- Click the save button

- Now visit the portal with the configured Url and you should see the default jquery.mobile based theme.

Add a new theme
---------------

You can add new jquery.mobile based themes. This is easily done via the `jquery.mobile Themeroller <http://https://themeroller.jquerymobile.com/>`_.

- Open your browser and point it to `<https://themeroller.jquerymobile.com>`_.

- Use the themeroller to make customisation for swatch **A** (the left one). This is easily done by drag and drop colors to the demo area.

- If you are finished, click the **Download theme zip file** Button at the top of the themeroller.

- Enter the Theme Name, for example **DemoTheme** and click **Download Zip**

- Now open your Plone instance and open **zettwerk.mobile Themes** in your Site Setup.

- Click the Browse Button to choose you recently downloaded jquery.mobile based Theme and click **Save**.

- The new theme gets automatically activated and should be visible when you reload your Mobile URL.


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


Examples
--------

- Screencast showing the installation and creation a Demo App: `zettwerk.mobile + zettwerk.mobiletheming + phonegap for Plone <https://www.youtube.com/watch?v=Q2ID86XkiQQ>`_

- Screencast showing the integartion of jquery.mobile based themes: `zettwerk.mobile with jquery.mobile's themeroller support for #plone <https://www.youtube.com/watch?v=s7n0IMjltzU>`_

- Demo Portal with activated theme: `http://mobile-demo.zettwerk.com <http://mobile-demo.zettwerk.com>`_.

- Demo APK (Android App) that points to the Demo Portal: `HelloWorld-debug.apk <https://github.com/macagua/plone_site_into_mobile/raw/master/HelloWorld-debug.apk>`_.
