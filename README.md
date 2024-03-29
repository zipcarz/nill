nill
====
Diff suppressed. Click to show.
612  javascript/playground.html
@@ -0,0 +1,612 @@
+<!DOCTYPE html>
+<html lang="en">
+    <head>
+        <meta name="viewport" content="width=700,maximum-scale=1.0,user-scalable=yes">
+        <title>Vimeo Froogaloop API Playground</title>
+        <style>
+            body, html, dl, dd { margin: 0; padding: 0;}
+
+            body, html {
+                font-family: "Helvetica Neue", Helvetica, Arial, Geneva, sans-serif;
+                color: #343434;
+                background: #f7f7f7;
+            }
+
+            iframe {
+                display:block;
+                border:0;
+                margin-bottom: 20px;
+            }
+
+            h1 {
+                font-weight: normal;
+                text-align: center;
+            }
+
+            button {
+                background: #e9e9e9;
+                cursor: pointer;
+                border: 1px solid #ddd;
+                padding: 2px 13px;
+                -webkit-border-radius: 3px;
+                -moz-border-radius: 3px;
+                margin: 0;
+                cursor: pointer;
+            }
+
+            .wrapper {
+                width: 600px;
+                margin: 0 auto;
+                margin-bottom: 30px;
+            }
+
+            .wrapper .container > div {
+                background: #fff;
+                padding: 30px;
+                border: 1px solid #ddd;
+                box-sizing: border-box;
+                margin-top: 30px;
+            }
+
+            .wrapper .container:first-child {
+                margin-top: 0;
+            }
+
+            .wrapper .container h2 {
+                margin: 0 0 20px 0;
+            }
+
+            .wrapper .container button {
+                line-height: 19px;
+            }
+
+            .wrapper .container input[type="text"] {
+                font-size: 12px;
+            }
+
+            button input[type="text"] {
+                border: 1px solid #ddd;
+                text-align: center;
+                -webkit-border-radius: 3px;
+                -moz-border-radius: 3px;
+                margin: 0 -11px 0 5px;
+                padding: 2px;
+            }
+
+            .wrapper div dl {
+                margin-bottom: 15px;
+            }
+
+            .wrapper div dt {
+                margin-bottom: 5px;
+            }
+
+            .wrapper div dt span {
+                font-size: 0.9em;
+                color: #666;
+            }
+
+            .wrapper div dd {
+                display: inline-block;
+                font-size: 12px;
+                margin-bottom: 5px;
+            }
+
+            .wrapper div dd label {
+                margin-right: 10px;
+            }
+
+            .wrapper div .output {
+                display: block;
+                width: 100%;
+                height: 100px;
+                border: 1px solid #ddd;
+                overflow-y: auto;
+                font-size: 13px;
+                padding: 5px;
+                box-sizing: border-box;
+                line-height: 1.4em;
+                resize: vertical;
+                font-family: Inconsolata, Monaco, monospace;
+            }
+
+            .wrapper .container > button {
+                border: 1px solid #ddd;
+                font-weight: bold;
+                font-size: 1.2em;
+                margin: -1px 0 0 0;
+                border-top-left-radius: 0;
+                border-top-right-radius: 0;
+            }
+
+            .wrapper > button input[type="text"] {
+                padding: 6px;
+            }
+
+            .console dd {
+                width: 100%;
+                white-space: nowrap;
+            }
+
+            .console .clear {
+                margin-top: 10px;
+            }
+        </style>
+    </head>
+    <body>
+        <div class="wrapper">
+            <hgroup>
+                <h1>Vimeo Froogaloop API Playground</h1>
+            </hgroup>
+            <div class="container">
+                <div>
+                    <h2>Vimeo Player 1</h2>
+                    <iframe id="player_1" src="http://player.vimeo.com/video/7100569?api=1&amp;player_id=player_1" width="540" height="304" frameborder="0"></iframe>
+                    <dl class="simple">
+                        <dt>Simple Buttons <span>(buttons with simple API calls)</span></dt>
+                        <dd><button class="play">Play</button></dd>
+                        <dd><button class="pause">Pause</button></dd>
+                        <dd><button class="unload">Unload</button></dd>
+                    </dl>
+                    <dl class="modifiers">
+                        <dt>Modifier Buttons <span>(buttons that modify the player)</span></dt>
+                        <dd><button class="seek">Seek <input type="text" value="30" size="3" maxlength="3" /></button></dd>
+                        <dd><button class="volume">Volume <input type="text" value="0.5" size="3" maxlength="3" /></button></dd>
+                        <dd><button class="loop">Loop <input type="text" value="0" size="3" maxlength="3" /></button></dd>
+                        <dd><button class="color">Color <input type="text" value="00adef" size="5" /></button></dd>
+                        <dd><button class="randomColor">Random Color</button></dd>
+                    </dl>
+                    <dl class="getters">
+                        <dt>Getters <span>(buttons that get back a value; logged out in the console)</span></dt>
+                        <dd><button class="time">Current Time</button></dd>
+                        <dd><button class="duration">Duration</button></dd>
+                        <dd><button class="color">Color</button></dd>
+                        <dd><button class="url">URL</button></dd>
+                        <dd><button class="embed">Embed Code</button></dd>
+                        <dd><button class="paused">Paused</button></dd>
+                        <dd><button class="getVolume">Volume</button></dd>
+                        <dd><button class="height">Video Height</button></dd>
+                        <dd><button class="width">Video Width</button></dd>
+                    </dl>
+                    <dl class="listeners">
+                        <dt>Event Listeners</dt>
+                        <dd><label><input class="loadProgress" type="checkbox" checked />loadProgress</label></dd>
+                        <dd><label><input class="playProgress" type="checkbox" checked />playProgress</label></dd>
+                        <dd><label><input class="play" type="checkbox" checked />play</label></dd>
+                        <dd><label><input class="pause" type="checkbox" checked />pause</label></dd>
+                        <dd><label><input class="finish" type="checkbox" checked />finish</label></dd>
+                        <dd><label><input class="seek" type="checkbox" checked />seek</label></dd>
+                    </dl>
+                    <dl class="console">
+                        <dt>Console</dt>
+                        <dd><textarea class="output" readonly="readonly"></textarea><button class="clear">Clear</button></dd>
+                    </dl>
+                </div>
+                <button class="addClip" title="Add a new clip.">+ <input type="text" value="3718294" size="8" /></button>
+            </div>
+
+        <script src="froogaloop.js"></script>
+        <script>
+            (function(){
+
+                // Listen for the ready event for any vimeo video players on the page
+                var vimeoPlayers = document.querySelectorAll('iframe'),
+                    player;
+
+                for (var i = 0, length = vimeoPlayers.length; i < length; i++) {
+                    player = vimeoPlayers[i];
+                    $f(player).addEvent('ready', ready);
+                }
+
+                /**
+                 * Utility function for adding an event. Handles the inconsistencies
+                 * between the W3C method for adding events (addEventListener) and
+                 * IE's (attachEvent).
+                 */
+                function addEvent(element, eventName, callback) {
+                    if (element.addEventListener) {
+                        element.addEventListener(eventName, callback, false);
+                    }
+                    else {
+                        element.attachEvent(eventName, callback, false);
+                    }
+                }
+
+                /**
+                 * Called once a vimeo player is loaded and ready to receive
+                 * commands. You can add events and make api calls only after this
+                 * function has been called.
+                 */
+                function ready(player_id) {
+                    // Keep a reference to Froogaloop for this player
+                    var container = document.getElementById(player_id).parentNode.parentNode,
+                        froogaloop = $f(player_id),
+                        apiConsole = container.querySelector('.console .output');
+
+                    /**
+                     * Prepends log messages to the example console for you to see.
+                     */
+                    function apiLog(message) {
+                        apiConsole.innerHTML = message + '\n' + apiConsole.innerHTML;
+                    }
+
+                    /**
+                     * Sets up the actions for the buttons that will perform simple
+                     * api calls to Froogaloop (play, pause, etc.). These api methods
+                     * are actions performed on the player that take no parameters and
+                     * return no values.
+                     */
+                    function setupSimpleButtons() {
+                        var buttons = container.querySelector('div dl.simple'),
+                            playBtn = buttons.querySelector('.play'),
+                            pauseBtn = buttons.querySelector('.pause'),
+                            unloadBtn = buttons.querySelector('.unload');
+
+                        // Call play when play button clicked
+                        addEvent(playBtn, 'click', function() {
+                            froogaloop.api('play');
+                        }, false);
+
+                        // Call pause when pause button clicked
+                        addEvent(pauseBtn, 'click', function() {
+                            froogaloop.api('pause');
+                        }, false);
+
+                        // Call unload when unload button clicked
+                        addEvent(unloadBtn, 'click', function() {
+                            froogaloop.api('unload');
+                        }, false);
+                    }
+
+                    /**
+                     * Sets up the actions for the buttons that will modify certain
+                     * things about the player and the video in it. These methods
+                     * take a parameter, such as a color value when setting a color.
+                     */
+                    function setupModifierButtons() {
+                        var buttons = container.querySelector('div dl.modifiers'),
+                            seekBtn = buttons.querySelector('.seek'),
+                            volumeBtn = buttons.querySelector('.volume'),
+                            loopBtn = buttons.querySelector('.loop'),
+                            colorBtn = buttons.querySelector('.color'),
+                            randomColorBtn = buttons.querySelector('.randomColor');
+
+                        // Call seekTo when seek button clicked
+                        addEvent(seekBtn, 'click', function(e) {
+                            // Don't do anything if clicking on anything but the button (such as the input field)
+                            if (e.target != this) {
+                                return false;
+                            }
+
+                            // Grab the value in the input field
+                            var seekVal = this.querySelector('input').value;
+
+                            // Call the api via froogaloop
+                            froogaloop.api('seekTo', seekVal);
+                        }, false);
+
+                        // Call setVolume when volume button clicked
+                        addEvent(volumeBtn, 'click', function(e) {
+                            // Don't do anything if clicking on anything but the button (such as the input field)
+                            if (e.target != this) {
+                                return false;
+                            }
+
+                            // Grab the value in the input field
+                            var volumeVal = this.querySelector('input').value;
+
+                            // Call the api via froogaloop
+                            froogaloop.api('setVolume', volumeVal);
+                        }, false);
+
+                        // Call setLoop when loop button clicked
+                        addEvent(loopBtn, 'click', function(e) {
+                            // Don't do anything if clicking on anything but the button (such as the input field)
+                            if (e.target != this) {
+                                return false;
+                            }
+
+                            // Grab the value in the input field
+                            var loopVal = this.querySelector('input').value;
+
+                            //Call the api via froogaloop
+                            froogaloop.api('setLoop', loopVal);
+                        }, false);
+
+                        // Call setColor when color button clicked
+                        addEvent(colorBtn, 'click', function(e) {
+                            // Don't do anything if clicking on anything but the button (such as the input field)
+                            if (e.target != this) {
+                                return false;
+                            }
+
+                            // Grab the value in the input field
+                            var colorVal = this.querySelector('input').value;
+
+                            // Call the api via froogaloop
+                            froogaloop.api('setColor', colorVal);
+                        }, false);
+
+                        // Call setColor with a random color when random color button clicked
+                        addEvent(randomColorBtn, 'click', function(e) {
+                            // Don't do anything if clicking on anything but the button (such as the input field)
+                            if (e.target != this) {
+                                return false;
+                            }
+
+                            // Generate a random color
+                            var colorVal = Math.floor(Math.random() * 16777215).toString(16);
+
+                            // Call the api via froogaloop
+                            froogaloop.api('setColor', colorVal);
+                        }, false);
+                    }
+
+                    /**
+                     * Sets up actions for buttons that will ask the player for something,
+                     * such as the current time or duration. These methods require a
+                     * callback function which will be called with any data as the first
+                     * parameter in that function.
+                     */
+                    function setupGetterButtons() {
+                        var buttons = container.querySelector('div dl.getters'),
+                            timeBtn = buttons.querySelector('.time'),
+                            durationBtn = buttons.querySelector('.duration'),
+                            colorBtn = buttons.querySelector('.color'),
+                            urlBtn = buttons.querySelector('.url'),
+                            embedBtn = buttons.querySelector('.embed'),
+                            pausedBtn = buttons.querySelector('.paused'),
+                            getVolumeBtn = buttons.querySelector('.getVolume'),
+                            widthBtn = buttons.querySelector('.width'),
+                            heightBtn = buttons.querySelector('.height');
+
+                        // Get the current time and log it to the API console when time button clicked
+                        addEvent(timeBtn, 'click', function(e) {
+                            froogaloop.api('getCurrentTime', function (value, player_id) {
+                                // Log out the value in the API Console
+                                apiLog('getCurrentTime : ' + value);
+                            });
+                        }, false);
+
+                        // Get the duration and log it to the API console when time button clicked
+                        addEvent(durationBtn, 'click', function(e) {
+                            froogaloop.api('getDuration', function (value, player_id) {
+                                // Log out the value in the API Console
+                                apiLog('getDuration : ' + value);
+                            });
+                        }, false);
+
+                        // Get the embed color and log it to the API console when time button clicked
+                        addEvent(colorBtn, 'click', function(e) {
+                            froogaloop.api('getColor', function (value, player_id) {
+                                // Log out the value in the API Console
+                                apiLog('getColor : ' + value);
+                            });
+                        }, false);
+
+                        // Get the video url and log it to the API console when time button clicked
+                        addEvent(urlBtn, 'click', function(e) {
+                            froogaloop.api('getVideoUrl', function (value, player_id) {
+                                // Log out the value in the API Console
+                                apiLog('getVideoUrl : ' + value);
+                            });
+                        }, false);
+
+                        // Get the embed code and log it to the API console when time button clicked
+                        addEvent(embedBtn, 'click', function(e) {
+                            froogaloop.api('getVideoEmbedCode', function (value, player_id) {
+                                // Use html entities for less-than and greater-than signs
+                                value = value.replace(/</g, '&lt;').replace(/>/g, '&gt;');
+
+                                // Log out the value in the API Console
+                                apiLog('getVideoEmbedCode : ' + value);
+                            });
+                        }, false);
+
+                        // Get the paused state and log it to the API console when time button clicked
+                        addEvent(pausedBtn, 'click', function(e) {
+                            froogaloop.api('paused', function (value, player_id) {
+                                // Log out the value in the API Console
+                                apiLog('paused : ' + value);
+                            });
+                        }, false);
+
+                        // Get the paused state and log it to the API console when time button clicked
+                        addEvent(getVolumeBtn, 'click', function(e) {
+                            froogaloop.api('getVolume', function (value, player_id) {
+                                // Log out the value in the API Console
+                                apiLog('volume : ' + value);
+                            });
+                        }, false);
+
+                        // Get the paused state and log it to the API console when time button clicked
+                        addEvent(widthBtn, 'click', function(e) {
+                            froogaloop.api('getVideoWidth', function (value, player_id) {
+                                // Log out the value in the API Console
+                                apiLog('getVideoWidth : ' + value);
+                            });
+                        }, false);
+
+                        // Get the paused state and log it to the API console when time button clicked
+                        addEvent(heightBtn, 'click', function(e) {
+                            froogaloop.api('getVideoHeight', function (value, player_id) {
+                                // Log out the value in the API Console
+                                apiLog('getVideoHeight : ' + value);
+                            });
+                        }, false);
+                    }
+
+                    /**
+                     * Adds listeners for the events that are checked. Adding an event
+                     * through Froogaloop requires the event name and the callback method
+                     * that is called once the event fires.
+                     */
+                    function setupEventListeners() {
+                        var checkboxes = container.querySelector('.listeners'),
+                            loadProgressChk = checkboxes.querySelector('.loadProgress'),
+                            playProgressChk = checkboxes.querySelector('.playProgress'),
+                            playChk = checkboxes.querySelector('.play'),
+                            pauseChk = checkboxes.querySelector('.pause'),
+                            finishChk = checkboxes.querySelector('.finish'),
+                            seekChk = checkboxes.querySelector('.seek');
+
+                        function onLoadProgress() {
+                            if (loadProgressChk.checked) {
+                                froogaloop.addEvent('loadProgress', function(data) {
+                                    apiLog('loadProgress event : ' + data.percent + ' : ' + data.bytesLoaded + ' : ' + data.bytesTotal + ' : ' + data.duration);
+                                });
+                            }
+                            else {
+                                froogaloop.removeEvent('loadProgress');
+                            }
+                        }
+
+                        function onPlayProgress() {
+                            if (playProgressChk.checked) {
+                                froogaloop.addEvent('playProgress', function(data) {
+                                    apiLog('playProgress event : ' + data.seconds + ' : ' + data.percent + ' : ' + data.duration);
+                                });
+                            }
+                            else {
+                                froogaloop.removeEvent('playProgress');
+                            }
+                        }
+
+                        function onPlay() {
+                            if (playChk.checked) {
+                                froogaloop.addEvent('play', function(data) {
+                                    apiLog('play event');
+                                });
+                            }
+                            else {
+                                froogaloop.removeEvent('play');
+                            }
+                        }
+
+                        function onPause() {
+                            if (pauseChk.checked) {
+                                froogaloop.addEvent('pause', function(data) {
+                                    apiLog('pause event');
+                                });
+                            }
+                            else {
+                                froogaloop.removeEvent('pause');
+                            }
+                        }
+
+                        function onFinish() {
+                            if (finishChk.checked) {
+                                froogaloop.addEvent('finish', function(data) {
+                                    apiLog('finish');
+                                });
+                            }
+                            else {
+                                froogaloop.removeEvent('finish');
+                            }
+                        }
+
+                        function onSeek() {
+                            if (seekChk.checked) {
+                                froogaloop.addEvent('seek', function(data) {
+                                    apiLog('seek event : ' + data.seconds + ' : ' + data.percent + ' : ' + data.duration);
+                                });
+                            }
+                            else {
+                                froogaloop.removeEvent('seek');
+                            }
+                        }
+
+                        // Listens for the checkboxes to change
+                        addEvent(loadProgressChk, 'change', onLoadProgress, false);
+                        addEvent(playProgressChk, 'change', onPlayProgress, false);
+                        addEvent(playChk, 'change', onPlay, false);
+                        addEvent(pauseChk, 'change', onPause, false);
+                        addEvent(finishChk, 'change', onFinish, false);
+                        addEvent(seekChk, 'change', onSeek, false);
+
+                        // Calls the change event if the option is checked
+                        // (this makes sure the checked events get attached on page load as well as on changed)
+                        onLoadProgress();
+                        onPlayProgress();
+                        onPlay();
+                        onPause();
+                        onFinish();
+                        onSeek();
+                    }
+
+                    /**
+                     * Sets up actions for adding a new clip window to the page.
+                     */
+                    function setupAddClip() {
+                        var button = container.querySelector('.addClip'),
+                            newContainer;
+
+                        addEvent(button, 'click', function(e) {
+                            // Don't do anything if clicking on anything but the button (such as the input field)
+                            if (e.target != this) {
+                                return false;
+                            }
+
+                            // Gets the index of the current player by simply grabbing the number after the underscore
+                            var currentIndex = parseInt(player_id.split('_')[1]),
+                                clipId = button.querySelector('input').value;
+
+                            newContainer = resetContainer(container.cloneNode(true), currentIndex+1, clipId);
+
+                            container.parentNode.appendChild(newContainer);
+                            $f(newContainer.querySelector('iframe')).addEvent('ready', ready);
+                        });
+
+                        /**
+                         * Resets the duplicate container's information, clearing out anything
+                         * that doesn't pertain to the new clip. It also sets the iframe to
+                         * use the new clip's id as its url.
+                         */
+                        function resetContainer(element, index, clipId) {
+                            var newHeading = element.querySelector('h2'),
+                                newIframe = element.querySelector('iframe'),
+                                newCheckBoxes = element.querySelectorAll('.listeners input[type="checkbox"]'),
+                                newApiConsole = element.querySelector('.console .output'),
+                                newAddBtn = element.querySelector('.addClip');
+
+                            // Set the heading text
+                            newHeading.innerText = 'Vimeo Player ' + index;
+
+                            // Set the correct source of the new clip id
+                            newIframe.src = 'http://player.vimeo.com/video/' + clipId + '?api=1&player_id=player_' + index;
+                            newIframe.id = 'player_' + index;
+
+                            // Reset all the checkboxes for listeners to be checked on
+                            for (var i = 0, length = newCheckBoxes.length, checkbox; i < length; i++) {
+                                checkbox = newCheckBoxes[i];
+                                checkbox.setAttribute('checked', 'checked');
+                            }
+
+                            // Clear out the API console
+                            newApiConsole.innerHTML = '';
+
+                            // Update the clip ID of the add clip button
+                            newAddBtn.querySelector('input').setAttribute('value', clipId);
+
+                            return element;
+                        }
+                    }
+
+                    setupSimpleButtons();
+                    setupModifierButtons();
+                    setupGetterButtons();
+                    setupEventListeners();
+                    setupAddClip();
+
+                    // Setup clear console button
+                    var clearBtn = container.querySelector('.console button');
+                    addEvent(clearBtn, 'click', function(e) {
+                        apiConsole.innerHTML = '';
+                    }, false);
+
+                    apiLog(player_id + ' ready!');
+                }
+            })();
+        </script>
+    </body>
+</html>
