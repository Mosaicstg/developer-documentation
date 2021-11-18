# LiquidWeb to Flywheel migration

## Table of Contents

- [Create Backups](#create-backups)
    - [Managed WP Hosting](#managed-wp-hosting)
- [Create Site on Flywheel](#create-site-on-flywheel)
## Create Backups

### Managed WP Hosting:

- Log into Managed LW WP hosting dashboard: https://app.getflywheel.com/org/mosaic/nj-shares (yes...that's really the URL for the dashboard)
- Go to installation's overview by clicking on the site's name in list of sites shown in the dashboard
- Go to **Backups** tab and initiate a backup by clicking `Create a New Backup`
    - In the event, that you'd like to have a copy of the backup you've just created click `Download Backup` on the far right of the row of the backup

## Create Site on Flywheel

- Log into the Flywheel dashboard: https://app.getflywheel.com/ (see how much friendlier this URL is...)
- Click the `Sites` link in the header
- Click the `CREATE A NEW SITE' button link and fill out the form

### Force HTTPS

- Once you've created the site visit the dashboard of the site you've just created
- Go to the `Advanced` tab
- Scroll down and turn of the `Force HTTPS` option

## Install Flywheel Migration Plugin (on source/origin site)

- Login into the WP dashboard of the site you'd like to migrate
- Go to **Plugins** > **Add New**
- Search and install **Flywheel Migrations** plugin
