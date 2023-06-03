 - When developers wish to submit software to the community, they will submit it to an  "apt" repository. 
 - **Additional repo can be added using this command** - `add-apt-repository` or listing another provider(some vendors will have a repository that is closer to their geographical location.)
 - the benefits of apt means that whenever we update our system -- the repository that contains the pieces of software that we add also gets checked for updates.
 - When adding software, the integrity of what we download is guaranteed by the use of what is called GPG (Gnu Privacy Guard) keys. These keys are essentially a safety check from the developers saying, "here's our software". If the keys do not match up to what your system trusts and what the developers used, then the software will not be downloaded.

## Managing Your Repositories (Adding and Removing)
