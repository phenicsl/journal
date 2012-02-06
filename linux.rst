Cookbooks
=========

Delete Entry from cscope.files
------------------------------

When generated cscope files by *find* command, there are some symbol link that
will be warned with "can not find file" error. Following process will help to
get ride of those annoying errors::

    for entry in /path/to/file1 /path/to/file2
    do
        entry=$(echo entry | sed -e 's#/#\\/#')    #escape '/'
	sed -i -e "/$entry/d" cscope.files
    done

Firstly, you have to escape '/' character since *sed* requires to use '/' as
delimiter in the address part. 

Secondly, a in-place edit option is specified here to replace 'cscope.files' in
place. 

After some study, I also found that you may use *"\%$entry%d"* here to specify
the address without escaping the path delimiter.

