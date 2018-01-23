marketplace-metadata
====================

This project hosts the metadata related to plugins in Pentaho's Marketplace, both BA Server and Kettle (Pentaho Data Integration).  

You can learn more about Pentaho's BA Server Marketplace here:
http://github.com/pentaho/marketplace

You can learn more about the Kettle Marketplace here:
http://wiki.pentaho.com/display/EAI/Marketplace

How to register your plugin
---------------------------
* Step 1: Clone this repository
* Step 2: Update the marketplace.xml file with your market-entry
* Step 3: Submit a pull request to have your plugin reviewed for inclusion in both the marketplace plugins and [website](http://www.pentaho.com/marketplace/)!

XML Plugin Format
-----------------
The Marketplace XML is shared between Pentaho's BA Server and Kettle, but at 
this time there are some feature differences.  Each element below specifies whether it's available in the two marketplaces.

```xml
<market_entry>
  <id>MY_ID</id> <!-- The ID is used to uniquely identify this plugin in the system. Required (Both) -->
  <type>Platform</type> <!-- The type of the plugin tells the marketplace how to install the plugin, and where it's applicable. Required (Both)
                             Values include:
                               - Platform - Appears in the BA Server Marketplace
                               - Step, JobEntry, Partitioner, SpoonPlugin, Database, Repository, ImportRule, Mixed - Appears in Kettle
                        -->
  <name>My Plugin</name> <!-- The name of the plugin presented to the user. Required (Both) -->
  <!-- The category of the market entry. Used for facilitating search in the marketplace. (Both) 
       Values include:
         - Apps - Admin, Analysis, Dashboards, Data, Development
         - PDI Plugins - Connectivity, Data Mining, Data Profiling, Data Quality, Enhancements, Lifecycle Management, Lookup
         - Other - Language Packs, Theme, Visualizations
  -->
  <category> 
    <name>SubCategory</name>
    <parent>
      <name>MainCategory</name>
    </parent>
  </category>
  
  <description>My Description</description> <!-- The description of the plugin presented to the user (Both) -->
  <documentation_url>http://me.com/mydoc.html</documentation_url> <!-- a url to documentation about the plugin (Both) -->
  <author>Me</author> <!-- The name of the author of the plugin (Both) -->
  <author_url>http://me.com</author_url> <!-- The location of the author's website (BA Server only) -->
  <author_logo>http://me.com/logo.png</author_logo> <!-- The location of the author's logo (BA Server only) -->
  <dependencies>pluginA, pluginB, pluginC</dependencies> <!-- list of plugins required for the correct operation of this plugin (BA Server only) -->

  <img>myimage.png</img> <!-- an image representing your plugin, displayed in the Marketplace (BA Server only) -->
  <small_img>mysmallimg.png</small_img>  <!-- a small image representing your plugin, displayed in the Marketplace (BA Server only) -->
  <installation_notes>Install Notes</installation_notes> <!-- an optional set of notes that displays during install for a plugin (BA Server only) -->
  <forum_url>http://forums.me.com</forum_url> <!-- a link to the forum related to this plugin (PDI only) -->
  <cases_url>http://jira.me.com</cases_url> <!-- a link to the bug tracking system related to this plugin (Kettle only) -->
  <license_name>Apache License 2.0</license_name> <!-- the license used by the plugin (Kettle only) --> 
  <license_text>For more details see:
    http://www.apache.org/licenses/LICENSE-2.0.html</license_text> <!-- the license text of the plugin (Kettle only) -->
  <support_level>PROFESSIONALY_SUPPORTED</support_level> <!-- The Support level which is available for this plugin (Kettle Only) 
                                                              Values Include: 
                                                                PROFESSIONALLY_SUPPORTED
                                                                COMMUNITY_SUPPORTED
                                                                NOT_SUPPORTED
                                                          --> 
  <support_message>Supported by Me.</support_message> <!-- A Support Message (Kettle only) -->
  <support_organization>Me</support_organization> <!-- The organization claiming support (Kettle only) -->
  <support_url>http://me.com/support</support_url> <!-- The URL to learn more about support for this plugin (Spoon only)-->
  
  <!-- The BA Server currently supports multiple versions of the same plugin with branches, Kettle currently does not, 
       only the first is read,  -->
  <versions>
    <version>
      <branch>Stable</branch> <!-- Tells the Marketplace what branch this plugin belongs to. Required (Both)  -->
      <version>1.0</version> <!-- The version of the plugin. Required (Both) -->
      <name>1.0</name> <!-- A User friendly name for the plugin (BA Server only) -->
      <package_url>http://me.com/plugin.zip</package_url> <!-- The download URL of the actual plugin (Both) -->
      <samples_url>http://me.com/plugin.zip</samples_url> <!-- The download URL of samples for this plugin (BA Server only) -->
      <description>My Version Description</description> <!-- the description of the specific version (BA Server only) -->
      <changelog>Changes</changelog> <!-- a list of changes since the last update (BA Server only) -->
      <build_id>12<build_id> <!-- If two versions of a plugin have the same version, you can still distinguish them using the build id - useful for trunk-snapshot versions (BA Server only) -->
      
      <!-- In the BA Server, if you specify min and max parent versions, the plugin will only appear in the 
           marketplace if the BA Server  is within range of those versions. -->
      
      <min_parent_version>3.8</min_parent_version> <!-- the minimum system version this plugin is compatible with (BA Server only) -->
      <max_parent_version>4.8</max_parent_version> <!-- the maximum system version this plugin is compatible with (BA Server only) -->
      <development_stage> <!-- the maturity classification of this version (Both) -->
        <lane>Community</lane>
        <phase>3</phase>
      </development_stage>
    </version>
  </versions>
  <screenshots> <!-- List of screenshots (up to 3) - BA Server Only -->
    <screenshot>screenshot_1.png</screenshot>
    <screenshot>screenshot_2.png</screenshot>
  </screenshots>
</market_entry>
```

What is the review process for the plugin?
------------------------------------------
At this time, the review process is informal, and can be done by any of the core 
committers of the marketplace-metadata project.  The core committers will review 
the plugin submission, and if accepted, will accept the pull request.

  
Version.xml: What is it and why should I use it?
------------------------------------------
 
version.xml is a file used by marketplace to determine which version of your plugin your user has installed.
This will allow the marketplace to tell the user when a new version is available and he can update your plugin.
The version.xml file should be located in the plugin root folder (where plugin.xml is) and it must follow
the following format:

    <version branch='<branch>' buildId='<buildId>'><versionNumber></version>

 * &lt;branch&gt; - This should be the branch from where this build originated (stable or trunk, but you can use 
 whatever you want - GA, RC, etc)
 * &lt;versionNumber&gt; - The plugin version. Can be a complex string
 *  &lt;buildId&gt; - This is used to differentiate between two versions who share the same version number. For instance,
 snapshot builds that usually have the same version (TRUNK-SNAPSHOT) can still be distinguished if the buildId is
 different. 
 
###Development Stage

The development stage is a project maturity classification with a two-lane approach.

* __Customer Lane__: Always overseen by PM and Engineering, projects in the Customer Lane can either start as customer-sponsored initiatives or as projects developed in the Community Lane that create value for Pentaho subscription customers. Pentaho will provide official support based on current support policies to projects on the Customer Lane.
   1. Development Phase: Start up phase of an internal project. Usually a Labs experiment.
   2. Snapshot Release: Unstable and unsupported branch, not recommended for production use.
   3. Limited Release: Assistence given by Services Development with no contractual support for production environments.
   4. Production Release: Production release with PM assigned, fully supported as part of the Pentaho release cycle. 
* __Community Lane__: The Community Lane will be used for projects created by Pentaho Consulting or Engineering Services, in which case they will be managed so they do not conflict with the long-term architecture and functionality planned in the Pentaho product roadmap.
  1. Development Phase: Start up phase of an internal project. Usually a Labs experiment.
  2. Snapshot Release: Unstable and unsupported branch, not recommended for production use.
  3. Stable Release: Adoption is ramping up and product could be used in production environments.
  4. Mature Release: Indicates a successfully adopted project in a mature state. 
  
How do I develop a plugin?
--------------------------
Link to BA Server Plugin Documentation:
http://wiki.pentaho.com/display/ServerDoc2x/Developing+Plugins

Link to the Pentaho InfoCenter SDK "Extending Pentaho Data Integration"
http://infocenter.pentaho.com/help/topic/pdi_embed_extend_guide/concept_extending_PDI.html

How do I test a marketplace entry ?
-----------------------------------
Create a file marketplaces.xml in your .kettle folder
The content of this file will be :

    <marketplaces>
        <marketplace>
            <name>Pentaho Data Integration Marketplace</name>
                <entries_url>{local path to your marketplace.xml file}</entries_url>
        </marketplace>
    </marketplaces>



Example :

    <marketplaces>
        <marketplace>
            <name>Pentaho Data Integration Marketplace</name>
                <entries_url>/home/matt/git/pentaho/marketplace-metadata/marketplace.xml</entries_url>
        </marketplace>
    </marketplaces>

