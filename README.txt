Viewmode per Node module
======================================================

DESCRIPTION
------------
This module provides the possibility to select inside every node edit form
the view mode to display its content. View modes is a feature of Drupal since
version 6, and it has a lot of power but normal admin user have no access to
all the possibilities. Basically this power consists on the possibility to have
several ways to organize the node display. Usually modules provide with new view
modes but user have any managing area for it. Moreover, users are allowed to
decide which views modes are active and which fields distribution they want on
each view mode, but the weak point of the system is that they are not allowed to
decide when to use one view mode or another. Only views allows to render full
nodes, and choose in which view mode, but that feature does not unleash its power.

But which escenarios may be useful to cover with this module? Imagine that the
editors on some site would like to decide to fit several displays for a node type,
on some cases main picture would be the first item, on other nodes first would be
the video, on other ones some list for related content would go on top. With
"Viewmode per Node" they could creat several view modes, organize the fields on
each and select on each individual node which view mode use to have on top the 
more interesting element.

The point that this module does not cover is creating new view modes. This feature
is very well covered by "Entity view mode", which in fact is a depency (without
that module this one won't be allowed to be installed). It has to be provided a
way to create new view modes anb "Entity view mode" covers that area very well,
with a very interesting features set, good UI (at least it fits very well Drupal
standards), comes from a respected and experienced community member and has a very
high number of reported installs.

But one of the things I like very much about "Entity view mode" is its very low size,
which added to the very small size of "Viewmode per Node" means a very interesting
alternative to "Display Suite", another solution to solve what this module proposes
but with a very large memory footprint.

ALTERNATIVES
------------
There is only one alternative to this module "Display Suite" using the module "Extras",
but this means loading your system memory with big modules that may be a problem on
some shared hostings. It gives lots of features that maybe you're not interested on
(or maybe you are): https://www.drupal.org/project/ds

"View Mode Page" (https://www.drupal.org/project/view_mode_page) builds a tab on
each node where renders the node on each view mode that is active for that node.

"View Mode Modal" (https://www.drupal.org/project/view_mode_modal) renders node on
the selected view mode inside CTools modal windows.

"Entity reference plus data" (https://www.drupal.org/project/er_plus) allows to
select the view mode of a node reference fiels when you are selecting the reference
on the node edit form.

With "Contextual View Modes" (https://www.drupal.org/project/contextual_view_modes)
it's even possible go one step further: you can select inside each node the view
mode you want to see it rendered depending on the context is active. I'm a huge
fan of context, I use it almost on every site, and this feature is a great tool
for many situations. The problem is that it depends on "Display Suite", it would
be great that it was capable to work also with "Entity view mode". It's possible
to define inside each node several conditions based on several context.

If memory on your site is a problem and you are used to code, maybe you can delete
the "Entity view mode" dependency on the .info file before installing and add at
the end of the .module file the next function:

/**
* Implements hook_entity_info_alter().
*/
function viewmode_per_node_entity_info_alter(&$entity_info) {
  $entity_info['node']['view modes']['special_display'] = array(
    'label' => t('Special display'),
    'custom settings' => TRUE,
  );
}

This is the "coding way" of adding new view mode, that easy! You can go to that
function whenever you want to add new mode to the array, and remember to clear
your cache before.

REQUIREMENTS
------------
1. Drupal 7.17 or higher. This module is based on "hook_entity_view_mode_alter()"
   which appeared on the this release. Upgrade your Drupal to the last version
   available, since is a good strategy to be bug free and with the most secure
   version of code.

2. "Entity view mode" (http://drupal.org/project/entity_view_mode) which is the
   best tool for creating new view modes, for your nodes and for whatever other entity.

INSTALLATION
------------
1. Place the module into your modules directory.
   This is normally the "sites/all/modules" directory.
   This module creates a new table on your data base with the name "viewmode_per_node".

2. Go to admin/build/modules. Enable the modules, it's on the "Fields" group.
   The "Viewmode per Node" modules is found in the Fields section.

Read more about installing modules at http://drupal.org/node/70151

USE
------------
3. Probably the first thing is planning very carefully all the view modes a site is
   going to need.

4. Afterwards you'll need to create them with "Entity view mode" on its configuration
   area: "yoursite/admin/config/system/entity-view-modes" (Configuration page, right
   column System pane).
   
5. Go to your content type structure at the "manage content" tab to ajust fields
   display: "yoursite/admin/structure/types/manage/destacado/display". Below the
   fields area you have a list of view modes, activate the ones you have created.
   Once they are active you'll see a list of subtabs under the title of this admin page.
   Select each one, set your fields configuration and save. Now you have all your
   view modes adjusted and ready to be selected.
   
6. Now go to each of your nodes, edit them and go to the workflow tabs below all the
   fields on the form. One of this tabs is "View Mode per Node", and inside there is
   a simple select menu "View modes" with the list of your view modes.

7. Select the view mode your interested for that node and Save. Look at the rendered
   node to see the different fields arranged on the order and configuration you decided.

8. Edit again and try other view modes selection to see the differences.   

AUTHOR
-------
Jordi Trujillo Rius - http://drupal.org/user/25348 (jorditr@innodus.com)
www.innodus.com

VERSIONS
--------
1.0.1 - first release (21 agost 2014)
1.0.2 - first release (22 agost 2014) - readme file and style corrections