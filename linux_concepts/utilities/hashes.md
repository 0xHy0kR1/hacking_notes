### Integrity
- When talking about integrity, we refer to the capacity we have to ascertain that a piece of data remains unmodified.
- you will often see a **hash** sent alongside the file so that you can prove that the file you downloaded kept its integrity and wasn't modified in transit.
- **hash** - A hash or digest is simply a number that results from applying a specific algorithm over a piece of data.

**Example** - 
if you go WinSCP repo, you'll see that for each file available to download, there are some hashes published along:
![[linux_integrity_hash1.png]]
These hashes were precalculated by the creators of WinSCP so that you can check the file's integrity after downloading.

## Calculating hash of file
To calculate the different hashes in Linux, we can use the following commands:
![[linux_integrity_hash2.png]]
Since we got the same hashes, we can safely conclude that the file we downloaded is an exact copy of the one on the website.

**Note** - Modern browsers allow you to specify a hash along the library's URL so that the library code is executed only if the hash of the downloaded file matches the expected value. This security mechanism is called Subresource Integrity (SRI).

You can go to [https://www.srihash.org/](https://www.srihash.org/) to generate hashes for any library if needed.