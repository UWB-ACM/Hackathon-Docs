# wiki

MongoDB process: `sudo service mongod start`

Wiki.js commands: 

`node wiki start` = start wiki.js

`node wiki stop` = stop wiki.js

`node wiki restart` = restart wiki.js

`node wiki configure 1234` = activate GUI browser configuration where 1234 is the custom port. Use port 80 for webservers.

`node wiki configure` = default configuration on port 3000

`node wiki -V` = displays the version of wiki



### Solution to modal.* in front of js elements
Improper JSON serving
See [Localization Issue #475](https://github.com/Requarks/wiki/issues/475)
- [x] This issue has been solved

### To display changes to configuration file:

1.   Go into admin account on the wiki - settings - system info - flush and rebuild
2.   If changes not displayed, proceed with step 3 and 4
3.  `sudo service mongod restart`
4.  `sudo node wiki restart`

### Customize Page Structure and Appearance

To customize, access files under `wiki/server/views`
