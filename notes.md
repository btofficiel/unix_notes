# Unix System Admin Handbook Notes

## Chapter 1

#### man
This command searches for the man pages after being given a keyword. For example
<pre>
man -k <i>keyword</i>
</pre>
Man pages are stored in the directory **/usr/share/man**. Cached versions of man are stored in **/var/cache/man**

The default search path for **man** could be known by entering the following command

<pre>
man
</pre>

The search path could be altered by overriding the env variable as following
<pre>
export MANPATH=/home/share/localman:/usr/share/man
</pre>

### Determining whether some package is installed or not
We can determine if a binary is in our search path by using following command
<pre>
which <i>binary</i>
</pre>

If which can't find it, try whereis
<pre>
whereis <i>binary</i>
</pre>

Another alternative is **locate** which uses a compiled index to seacch for filenames using a given pattern
<pre>
locate <i>file</i>
</pre>

### Installing a package from source 
<pre>
cd /tmp

## Unzip or clone project_directory here

cd <i>project_directory</i>

./configure

make

sudo make install
</pre>

Using **--prefix=*directory*** we can specify the installation directory other than the default which is **/usr/local** 

