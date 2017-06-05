# vaadin-karaf
Using Vaadin 8.1 with Apache Karaf

* Install Apache Karaf 4.1: (http://karaf.apache.org/download.html)
* If necessary run $ 'chmod u+x ./karaf' in the bin folder of Karaf
* Run karaf $ './karaf' -> Wait a while, takes good 10 seconds to start

In Karaf: feature:list shows you all installed features.
* One the first run install 'http' and 'http-whiteboard' features:
 - $ 'feature:install http'
 - $ 'feature:install http-whiteboard'

* In Karaf: bundle:list shows you the list of Bundles
* One the first run install Vaadin dependency bundles:
 - bundle:install -s mvn:org.jsoup/jsoup/1.8.3
 - bundle:install -s mvn:com.vaadin.external/gentyref/1.2.0.vaadin1
 - bundle:install -s mvn:com.vaadin/vaadin-shared/8.1.0.beta1
 - bundle:install -s mvn:com.vaadin/vaadin-server/8.1.0.beta1
 - bundle:install -s mvn:com.vaadin/vaadin-osgi-integration/vaadin-osgi-integration-8.1.0.beta1
 - bundle:install -s mvn:com.vaadin/vaadin-client-compiled/8.1.0.beta1
 - bundle:install -s mvn:com.vaadin/vaadin-themes/8.1.0.beta1

* Run $ 'bundle:list', you should see all bundles active, if any of the bundles is in 'installed' state it means that it's missing dependencies. In this case type $ 'log:tail' to see what's going on inside Karaf.

* $ 'mvn install' the application from this git repository to your local maven repository

* Go back to Karaf and install the application $ 'bundle:install mvn:com.example/myapp/1.0-SNAPSHOT' Karaf can install it from your local Maven repo as well, which is nice.

* Run $ 'http:list', you should see a listing similar to this but with different IDs

ID  |Servlet           | Servlet-Name        | State       | Alias                                                             | Url                                                                    |
----|------------------|---------------------|-------------|-------------------------------------------------------------------|------------------------------------------------------------------------|
100 | ResourceServlet  | DefaultWidgetSet    | Deployed    | /vaadin-8.1.0.beta1/VAADIN/widgetsets/com.vaadin.DefaultWidgetSet | \[/vaadin-8.1.0.beta1/VAADIN/widgetsets/com.vaadin.DefaultWidgetSet/*\]|
99  | ResourceServlet  | gz                  | Deployed    | /vaadin-8.1.0.beta1/VAADIN/vaadinBootstrap.js.gz                  | \[/vaadin-8.1.0.beta1/VAADIN/vaadinBootstrap.js.gz/*\]                 |
109 | ResourceServlet  | /res                | Deployed    | /system/console/res                                               | \[/system/console/res/*\]                                              |
99  | ResourceServlet  | js                  | Deployed    | /vaadin-8.1.0.beta1/VAADIN/vaadinBootstrap.js                     | \[/vaadin-8.1.0.beta1/VAADIN/vaadinBootstrap.js/*\]                    |
109 | KarafOsgiManager | ServletModel-9      | Deployed    | /system/console                                                   | \[/system/console/*\]                                                  |
120 | MyUI$MyUIServlet | ServletModel-14     | Deployed    |                                                                   | \[/myapp/*\]                                                           |
101 | ResourceServlet  | /VAADIN/themes/valo | Deployed    | /vaadin-8.1.0.beta1/VAADIN/themes/valo                            | \[/vaadin-8.1.0.beta1/VAADIN/themes/valo/*\]                           |

* If any of the static resources etc. are missing, try updating the corresponding bundles with $ 'bundle:update 100' for example.
* Now you should be able to run the Vaadin app from localhost:8181/myapp
