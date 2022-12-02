# LAB REPORT 4

## PART 1

The following vim command sequence is used to change the name of the start parameter and its uses to base.

### Command Sequence:

`vim<space>D<tab><enter>/start<enter>cebase<esc>n.n.:wq<enter>`

### Breaking it down:

`vim<space>D<tab>` print the command on the command line

<img width="469" alt="image" src="https://user-images.githubusercontent.com/114612660/203975662-f1a6fc68-bf53-4ae8-920f-d5362ab246bd.png">

`/start` searches for the word `start`

<img width="187" alt="image" src="https://user-images.githubusercontent.com/114612660/203976298-4071447d-5827-4623-832f-5d6dbff8f907.png">

`<enter>` takes you to the location of word `start`

<img width="533" alt="image" src="https://user-images.githubusercontent.com/114612660/203976436-c97cf2b2-4f2b-4201-9588-9b30d27a9cb7.png">

`ce` switches to insert mode and deletes the word `start`

<img width="550" alt="image" src="https://user-images.githubusercontent.com/114612660/203976487-91742323-d045-4612-94ef-3aa102920b65.png">

`base<esc>` replaces the word with `base` and then returns to normal mode.

<img width="532" alt="image" src="https://user-images.githubusercontent.com/114612660/203976556-47622e59-57cb-440b-8fc9-bbfcd1e1c643.png">

`n.` will repeat the sequence, it finds the next location of `start` is and changes it to `base`.

<img width="498" alt="image" src="https://user-images.githubusercontent.com/114612660/205291416-508b7ac0-4ab6-4007-b4b9-46d6b7b4ac6d.png">

`n.` executes this sequence again.

<img width="686" alt="image" src="https://user-images.githubusercontent.com/114612660/203977128-58580c50-52bc-46c0-b155-c03f734490db.png">

`:wq` saves the file and exits the editor.

<img width="92" alt="image" src="https://user-images.githubusercontent.com/114612660/203977251-b2f32014-5562-4cc7-a561-0800b7854a04.png">

## PART 2

Using `scp` to send the edited file over to the remote server took **175 seconds**. <br/>
Using `vim` to make edits on the remote server took **73 seconds**. 

If I had to work on a program that I was running remotely, I would definitely prefer `vim` over scp. vim shortcuts make it easier to traverse a file and make changes. Creating files is also much faster using vim. Assuming that there are some changes to be made in a few files but the entire directory needs to be sent to the remote server, scp takes a very long time to send the files over. On the other hand, we can use vim to access the particular files that need to be changed and quickly edit them.

If, for any project or task, I would have to make a lot of code changes to **both** the local computer and the remote server, I would prefer using scp. scp would be more accurate in this case, as it sends the files over exactly. Using vim would mean that I would have to manually mimic changes to the other device which might be lesser accuarate and efficient. It is also much easier to change the code once and send it rather than editing it twice. 
