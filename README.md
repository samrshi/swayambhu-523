# Swayambhu Stories

COMP 523 Team D Client Project. Forked from https://github.com/potree/potree

## View Deployment

https://swayambhu-stories.cloudapps.unc.edu

## To Test Locally
1. Clone this repository
   ```
   git clone https://github.com/samrshi/swayambhu-523.git
   ```
2. Download all of the files and folders in this [Google Drive folder](https://drive.google.com/drive/folders/14X5wysWBXZyDzytmhLj998Q-qI3BdXTS?usp=sharing)
   > **Hint** - 
   > Click `comp 523 - swayambhu` in the toolbar at the top and then `Download` in the menu.
3. Place those files into `assets/`
   ```
   assets/
   - swayambhu-converted/
   - a0.mp3
   - prostrations.jpg
   - v0.mp4
   ```
4. Run the following sequence of commands
   ```
   npm i
   npm run build
   npm start
   ```
5. Open [`http://127.0.0.1:8080`](http://127.0.0.1:8080) to see the live preview

## Deployment Instructions
1. Push to the `main` branch of this repository
2. A build should automatically start in CloudApps
3. Verify that the build is running by opening the `swayambhu-stories` detail pane in the Topography section of the [CloudApps Console](https://console.apps.cloudapps.unc.edu)
4. If a new build hasn't yet started, click the `Start Build` button

## Adding to the `assets` Directory
You might notice that the `assets` directory's [`.gitignore`](./assets/.gitignore) hides all files in the folder from Git. This can make it a little bit complicated to add your own assets. So, if you'd like to make a change, follow these steps...

1. Follow [this guide](https://uncch.service-now.com/sp?id=kb_article_view&sysparm_article=KB0011218&sys_kb_id=29774cbedb90f01070551ffa68961958) to install the `oc` command line tools and add `oc` to your path
   > **Hint** - You may need to do some additional setup to add `oc` to your path
2. Log in to `oc` with the following command
   ```
   oc login -u <onyen> api.cloudapps.unc.edu
   ```
3. `cd` into this repository on your local machine
4. Add your desired files to your local `assets` folder
5. Run `oc get pods` to get a list of all pods. Copy the name of the currently running pod.
   > **Hint** - It should have a format something like `swayambhu-stories-[n]-[id]`
7. Use [`rsync`](https://www.digitalocean.com/community/tutorials/how-to-use-rsync-to-sync-local-and-remote-directories) to push those new files to the CloudApps persistent storage.
   > **Hint** - See the `Files` section of [this article](https://help.unc.edu/sp?sys_kb_id=2136cb72db5c341070551ffa6896197b&id=kb_article_view&sysparm_rank=2&sysparm_tsqueryId=e27179f71b1bd55078c43112cd4bcb03) for some more details.
   ```bash
   # Example command:
   oc rsync --progress assets <pod-name>:/opt/app-root/src/
   ```
8. You might not need to, but triggering a new build couldn't hurt
