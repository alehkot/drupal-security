Drupal Security
===============
Pieces of advice on how-to improve the security on your Drupal websites.

Hiding traits of Drupal
--
To secure your a website from automated attacks it always better to hide the CMS:
- By removing CHANGELOG.txt file;
- By removing GENERATOR meta-tag (e.g. using https://www.drupal.org/project/remove_generator module);
- By hiding PHP fatal errors  (e.g. using https://www.drupal.org/project/hide_php_fatal_error module);
- By renaming admin paths (e.g. using https://www.drupal.org/project/rename_admin_paths module);
- By modifying the template of robots.txt file;
- By disallowing viewing of txt files in the core folder;
- By modifying Drupal default Expires header;
- By renaming default Drupal strings (e.g. using String Overrides module);
- By renaming default classes in Drupal theme;
- By changing default upload paths;
- By creation of custom 403/404 pages;
- By removing, renaming and/or updating update.php file;
- By removing, renaming and/or updating cron.php file;
- By updating default images, e.g. throbber.

Handling [PSA-2014-003](https://www.drupal.org/PSA-2014-003) (Drupalgeddon)
---
 1. Immediately upgrade to Drupal 7.32, of it’s not possible at least patch the vulnerable function in /includes/database/database.inc file;
 2. Check files integrity using Git status or if not possible using Hacked;
 3. If possible, redeploy the latest version of the code base;
 4. Scan public / private files locations for *.php, *.sh and any other suspicious files. There are some strategies to improve this procedure: for instance, if only images uploads are allowed, then we scan scan for any files other than images;
 5. If the webserver setup is permissive in terms of permissions and users (e.g. Apache user can write anywhere), it will be additionally required to perform audit of the entire server;
 6. Install, Security review, Drupalgeddon, Site Audit contributed modules and execute these modules checks;
Set another Drupal hash salt in settings.file for passwords generation, reset passwords of all the users and send them new;
 7. If the pages are built using Features module and if allowed, then revert all the features to their original state;
 8. Rebuild the menu executing core ‘menu_rebuild()’ function;
 9. Review the `variable` table to find any suspicious values. On some installations it might be possible to truncate the table entirely, if Features module is used and if default values of variables are acceptable.
 10. Check the database for new MySQL users, update MySQL passwords and regenerate passwords/tokens for any systems, which are integrated;
 11. Check users’ roles to find if there is a user which have ‘admin’ role;
 12. Check `menu_router` and `users` tables for suspicious entries, e.g. with ‘file_put_contents’ callbacks;
 13. Dump the entire website HTML, e.g. using some crawler, and grep for additional parameters in links;
 14. If possible analyze sessions table for logins of admin/advanced users from external IP addresses and check their last login dates.
 15. Analyze Apache Logs for POST keys with strings 'UPDATE', 'INSERT', 'DELETE', ‘?q=node&destination=node’;
 16. Check places in Panels, Blocks, Views where custom PHP snippets might be used, e.g. in custom access rules.
 17. Set another Drupal hash salt in settings.file for passwords generation, reset passwords of all the users and send them new;
 18. Check the database for new MySQL users, update MySQL passwords and regenerate passwords/tokens for any systems, which are integrated.
