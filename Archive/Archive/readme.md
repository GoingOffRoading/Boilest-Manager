# Workflow

This is the Boilest workflow, and work that is currently outstanding 

# To Do List
- [x] Cron that checks the queue, and injects the find_files task if the queue is empty
- [x] Task that recusively searches directories based on file extensions
- [x] For each file, calls the next step
- [x] Function that calls FFprobe for the file, and determines next step
- [x] Function that calls FFmpeg and processes the file
- [x] Function that moves the encoded file into the source and deletes the soure file
- [x] Function that checks the files size of the new and old file
- [x] Configuration based
- [x] Writing results of the ffencode step to SQLite
- [x] Starts workflow based on a JSON configuration
- [x] Rewrite the FFProbe section to handle when a media file doesn't have a video, audio, or subtitle stream
- [x] Expirement with AV1 film grain: https://www.google.com/search?q=av1+film+grain+synthesis+anime
- [x] Fix an issue where invalid ffmpeg settings would crash ffmpeg, and a file of 0kb would replace source 
- [x] UI
- [x] When establishing the codecs, we check for keywords like 'video' (see line 91 in Taks.py), which may return a false positive because ffprobe could use the keyworld 'video' in objects not related to defining the stream type.  Will need to figure out how to work around this.
- [x] Add more inline documentation
- [x] Add additional fields so different file attributes can get different ffmpeg commands
- [x] Celery queues: https://stackoverflow.com/questions/51631455/how-to-route-tasks-to-different-queues-with-celery-and-django
- [X] Celery starts queues based on docker env variables
- [x] Around line 150 in tasks...  The function to check if ffmpeg should run checks for a variable like subtitle, without establishing if the subtitle stream exists.  This casues all media missing the stream to encode.  Need to fix.
- [ ] Repo Documentation
- [x] Add the other two SQL insert statements to fresults
- [x] Rearrange git repo/directory structure
- [x] Experiment with the Ubuntu FFMpeg image for SVT-AV! latest and greatest
- [x] Create and integrate a secrets/config file/template, or maybe use container evars
- [x] See if we can create a test pipeline using open source video clip
- [x] Sort through the test scrips, and start deleting duplicates
- [x] Rewrite the function that checks the queues as that is spagetti
- [x] Replace the print statements with logging: https://docs.python.org/3/howto/logging.html
- [x] Resolve issues with OPUS compatibility
- [x] Resolve issues where output = 0.0 but tries to get moved anyway
- [x] In each step, if we no longer need components of the JSON, delete them
- [x] Rewrite the ffprobe codec check loop to use variables from the config again
- [ ] Need to configure for AMPQ retries against RabbitMQ if RabbitMQ restarts
- [x] Need to figure out how to configure RabbitMQ for celery if RabbitMQ restarts
- [x] Figure out the correct permission level of the celery rabbitmq user to create/read/etc queues
- [x] Rewrite how Boilest starts, so that configs, and the DB, can be persisted
- [x] Change up flower so that it has authenticated API access (so that tasks can be deleted)
- [x] See if we can get ffmpeg to stream it's output to print or logs
- [ ] Reorganize the container startup so it's not such a mess
- [x] Determine if it would be better to copy the file being encoded to the encoding machine to deal with NFS errors
- [x] Determine if we could slow down the number of status messages from ffmpeg
- [x] Find a more elegant solution to overflowing the buffer than sys.stdout.flush().  Likely moot if I write to a log
- [x] Investigate the db lock issue
- [x] Fix the logic for calling ffresults
- [ ] Send failed queue to log file
- [x] When printing results, or the hold because of queue, print a timestamp
- [x] When printing results, print the size delta on the encoded file
- [x] Add timestamps to when tasks start and stop, or a duration on how long something has taken, tbd
- [ ] Consider adding additional logic on the DB check to check for the DB, then table, then fields
- [x] Break up the tasks into worker and manager, including queue changes
- [ ] Put together a Kubernetes PV, PVC for the shared media
- [ ] Make the log level a container variable
- [x] Adjust the ffresults to use the end file name, not the start file name, and add the start container to original string
- [x] Update the ffencode print statement to remove the ( )
- [x] Add a validation check on writing the results
- [x] Create a way for Boilest to not encode files that were changed after the last scan.  Either with a last modified check, empty the queue week... Something
- [ ] Write the logs to a file, or aggregate the logs somewhere
- [x] Take a second pass at adjusting the log evels of things
- [ ] Convert Celery.sh to python, and have all of the container start stuff be there
- [ ] Think about doing a queue length check so that the queue legnth isn't crazy
- [x] Think about generating a file hash (name + file size or something) on initial ffprobe so that the worker can confirm that the file is the same one that the manager scanned 
- [x] Consider lookin into queue priorty 
- [x] Move the default logging to warning (currently info)
- [ ] Consider modifying ffmpeg to export it's output to a file, and store that on the master node
- [x] Rethink queue_workers_if_queue_empty.  Specifically, can we keep the queue to like 100 tasks, and then just check the queue to see if that file is already represented there.
- [ ] Rewrite how AV1's settings are stored per directory.  Consider a YAML or etc for these configs.
- [ ] Rewrite how tasks are prioritized
- [X] Make adjustments to the log levels
- [ ] Change the logic to 'try' for anything interacting with a file
- [ ] Expirement with subtitle settings
- [ ] Experiement with audio codec settings
- [ ] Think about how the project is structured within the working directories
- [ ] Create startup scripts that check for the celery user, namespace, queues, and creates anything that doens't exist
- [ ] As part of manager start up, have it delete all tasks
- [ ] Cron to back up DB periodically
- [ ] Cron to delete completed tasks
- [ ] Rewrite manager to ffprobe and make decision on process a single function



https://ranvir.xyz/blog/using-celery-to-run-long-running-task-asynchronously/