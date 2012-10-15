marketplace-metadata
====================

This project hosts the metadata related to plugins in Pentaho's Marketplace, both BA Server and Spoon.  

You can learn more about Pentaho's BA Server Marketplace here:
http://github.com/pentaho/marketplace

You can learn more about Spoon's Marketplace here:
http://wiki.pentaho.com/display/EAI/Market

How to register your plugin
---------------------------
Step 1: Clone this repository
Step 2: Update the marketplace.xml file with your market-entry
Step 3: Submit a pull request to have your plugin reviewed for inclusion in the marketplace!

XML Plugin Format
-----------------
The Marketplace XML is shared between Pentaho's BA Server and Spoon, but at 
this time there are some feature differences.  Each element below specifies whether it's available in the two marketplaces.

<market_entry>
  <id>MY_ID</id> <!-- The ID is used to uniquely identify this plugin in the system (Both) -->
  <type>Platform</type> <!-- The type of the plugin tells the marketplace how to install the plugin, and where it's applicable. (Both)
                             Values include:
                               - Platform - Appears in the BA Server Marketplace
                               - Step, JobEntry, Partitioner, SpoonPlugin, Database, Repository, ImportRule, Mixed - Appears in Kettle
                        -->
  <name>My Plugin</name> <!-- The name of the plugin presented to the user (Both) -->
  <description>My Description</description> <!-- The description of the plugin presented to the user (Both) -->
  <documentation_url>http://me.com/mydoc.html</documentation_url> <!-- a url to documentation about the plugin (Both) -->
  <author>Me</author> <!-- The name of the author of the plugin (Both) -->
  <author_url>http://me.com</author_url> <!-- The location of the author's website (BA Server only) -->
  <author_logo>http://me.com/logo.png</author_logo> <!-- The location of the author's logo (BA Server only) -->
  
  <img>myimage.png</img> <!-- an image representing your plugin, displayed in the Marketplace (BA Server only) -->
  <small_img>mysmallimg.png</small_img>  <!-- a small image representing your plugin, displayed in the Marketplace (BA Server only) -->
  <installation_notes>Install Notes</installation_notes> <!-- an optional set of notes that displays during install for a plugin (BA Server only) -->
  <forum_url>http://forums.me.com</forum_url> <!-- a link to the forum related to this plugin (Spoon only) -->
  <cases_url>http://jira.me.com</cases_url> <!-- a link to the bug tracking system related to this plugin (Spoon only) -->
  <license_name>Apache License 2.0</license_name> <!-- the license used by the plugin (Spoon only) --> 
  <license_text>For more details see:
http://www.apache.org/licenses/LICENSE-2.0.html</license_text> <!-- the license text of the plugin (Spoon only) -->
  <support_level>PROFESSIONALY_SUPPORTED</support_level> <!-- The Support level which is available for this plugin (Spoon Only) 
                                                              Values Include: 
                                                                PROFESSIONALLY_SUPPORTED
                                                                COMMUNITY_SUPPORTED
                                                                NOT_SUPPORTED
                                                          --> 
  <support_message>Supported by Me.</support_message> <!-- A Support Message (Spoon only) -->
  <support_organization>Me</support_organization> <!-- The organization claiming support (Spoon only) -->
  <support_url>http://me.com/support</support_url> <!-- The URL to learn more about support for this plugin (Spoon only)-->
  
  <!-- The BA Server currently supports multiple versions of the same plugin with branches, Spoon currently does not, 
       only the first is read -->
  <versions>
    <version>
      <branch>Stable</branch> <!-- Tells the Marketplace what branch this plugin belongs to (BA Server only) -->
      <version>1.0</version> <!-- The version of the plugin (Both) -->
      <name>1.0</name> <!-- A User friendly name for the plugin (BA Server only) -->
      <package_url>http://me.com/plugin.zip</package_url> <!-- The download URL of the actual plugin (Both) -->
      <samples_url>http://me.com/plugin.zip</samples_url> <!-- The download URL of samples for this plugin (BA Server only) -->
      <description>My Version Description</description> <!-- the description of the specific version (BA Server only) -->
      <changelog>Changes</changelog> <!-- a list of changes since the last update (BA Server only) -->
      <build_id>12<build_id> <!-- I have no idea what this is (BA Server only) -->
      
      <!-- In the BA Server, if you specify min and max parent versions, the plugin will only appear in the 
           marketplace if the BA Server is within range of those versions. -->
      
      <min_parent_version>3.8</min_parent_version> <!-- the minimum system version this plugin is compatible with (BA Server only) -->
      <max_parent_version>4.8</max_parent_version> <!-- the maximum system version this plugin is compatible with (BA Server only) -->
    </version>
  </versions>
        
</market_entry>  

What is the review process for the plugin?
------------------------------------------
At this time, the review process is informal, and can be done by any of the core 
committers of the marketplace-metadata project.  The core committers will review 
the plugin submission, and if accepted, will accept the pull request.

  
How do I develop a plugin?
--------------------------
Link to BA Server Plugin Documentation:
http://wiki.pentaho.com/display/ServerDoc2x/Developing+Plugins

Link to PDI Plugin Documentation:
http://wiki.pentaho.com/display/EAI/Writing+your+own+Pentaho+Data+Integration+Plug-In