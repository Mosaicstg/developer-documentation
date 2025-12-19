# Drupal to WordPress

## Table of Contents

- [Export Drupal](#export-drupal)

## Export Drupal

### Pantheon

This sections assumes you have access to the hosting dashboard of a site on Pantheon.

1. Log on to the Pantheon dashboard
2. Click into the site you'd like to export
3. Click on the `Live` tab (this is the production environment of the site)
4. Click the `Backups` link in the left sidebar
5. Create a new backup of the site
6. Download the `Code`, `Database` and `Files` files for the backup you've just created
   - In some instances where the files are _really_ large the download may fail a few times based on your internet connection

## FG Drupal To WordPress

### Terminal Usage (via Terminus/Pantheon)

#### Run import

The following instructions assume:
- FG Drupal to WordPress (Premium) is installed on the WordPress installation.
- Terminus (Pantheon's proprietary CLI tool) is installed on your machine. If you do not have it installed [visit Pantheon's website](https://pantheon.io/docs/terminus) to install it.

1. Authenticate with terminus using with your machine token:
   `terminus auth:login --machine-token=[YOUR_MACHINE_TOKEN]`
   - To set up a machine token please [visit Pantheon's documentation website](https://pantheon.io/docs/machine-tokens).
2. Find the Pantheon site you're looking to access/run commands on
   `terminus site:list`
   - This will list all the sites your user profile has been given access to. If you don't see the site you're looking for then you need to request for a higher level of access.
3. Ensure you have the correct settings on the backend of WordPress for what content you'd like to migrate
   - On the site you're trying to import the Drupal content into ensure you've set the following:
     - Database connection settings
     - Media connection settings
     - Content settings
       - Media upload files
       - Custom Post Types
       - Custom taxonomies
4. Run the import:
   `terminus wp [SLUG_OF_SITE].[SITE_ENVIRONMENT] -- import-drupal import`



