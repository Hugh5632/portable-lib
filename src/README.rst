====================
Guide to source code
====================

This is a brief guide to the various files in this directory.

Xor Filter:

    - xorfilter.c - Better than Bloom & Cuckoo filters
    - xorfilter_marshal.c: Marshal, Unmarshal of Xorfilter

    Performance numbers on a Pixelbook Core i7:
    Xor8  10000 items::

        create 216.738 cy/elem, find 2304.860 cy/elem
        create   7.4 M ops/sec, find 0.7 M ops/sec

    Xor16 10000 items::

        create 223.628 cy/elem, find 2417.902 cy/elem
        create   7.2 M ops/sec, find 0.7 M ops/sec

Bloom Filter:

    - bloom.c: Core bloom filter code (standard, counting, scalable)
    - bloom_marshal.c: Marshal, Unmarshal of bloom filters

    Performance numbers on MacBook Pro 15,1 (Late 2018)::

        Standard Bloom filter: 155 cycles/add, 148 cycles/search
        Counting Bloom filter: 157 cycles/add, 150 cycles/search
        Scalable Bloom filter: 716 cycles/add, 770 cycles/search


Fast hash table:

    fast-ht.c: Fast hash table with chunked array of buckets.
    Takes full advantage of cacheline alignment: keys are
    `uint64_t` and values are `void*`. Some perf numbers on a
    MacBook Pro 15,1 (Late 2018) [6 Core i9 at 2.9GHz, 32GB of RAM]::

        insert: 148 cycles (~16M inserts/sec)
        find:   41 cycles  (~41M searches/sec)
        delete: 42 cycles  (~38M deletes/sec)
        find non existant entry: 39 cycles (~40M searches/sec)

Policy based hash table:

    - hashtab.c: Policy based hash table with dlink collision chain
    - hashtab_iter.c: Iterators for the hash table

Hash Functions:

    - cityhash.c: CityHash
    - fasthash.c: Zilong Tan's super fast hash
    - fnvhash.c: Fowler, Noll, Vo hash
    - hsieh_hash.c: Paul Hsieh's hash function
    - metrohash128.c: Google's Metrohash
    - metrohash128crc.c: Google's Metrohash
    - metrohash64.c: 64 bit Metrohash
    - murmur3_hash.c: Austin Appleby's Murmur hash
    - siphash24.c: DJB's Siphash-2-4
    - xxhash.c: Yann Collet's xxHash
    - yorrike.c: Derivative of FNV1a

Growable Strings:

    - gstring.c: Growable string functions
    - gstring_var.c: Variable expansion inside growable strings

Random number Generators:

    - abyssinian_rand.c: Abyssinian PRNG (32-bit output)
    - arc4random.c: Portable, thread-safe implementation of OpenBSD
      chacha20 arc4random.
    - frand.c: Generate random floating point numbers in the
      interval (0, 1.0)
    - rand_marsaglia.cpp: Marsaglia PRNG
    - mtrand.c: Mersenne Twister PRNG
    - xorshift.c: Xorshift 64*, Xorshift 128+, Xorshift 1024* PRNG
    - xoroshiro.c: Xoroshiro 128+ PRNG

Memory Allocators:

    - arena.c:  Object lifetime based memory allocator
    - mempool.c: Fixed size memory allocator
    - memmgr.c: Memory management policy wrapper (used by hash
      tables above).


Utility String functions:

    - splitargs.c: Split string into tokens and handle embedded
      quoted words.
    - str2hex.c:  Decode hex string into uint8*
    - strcasecmp.c: case insensitve string compare
    - strcopy.c: Safe string copy (a better ``strcpy(3)``)
    - strlcpy.c: OpenBSD's ``strlcpy(3)``
    - strsplit.c: Split a string by delimiters
    - strsplit_csv.c: Split a string containing CSV (comma separated
      values)
    - strtosize.c: Convert a string with size suffix into a number.
    - strtrim.c: Trim a string of whitespaces
    - strunquote.c: Remove starting and ending quotes (if any)

Other Utility Functions:

    - b64_decode.c: Base64 decoder
    - b64_encode.c: Base64 encoder
    - c_resolve.c: Resolve interfaces names & addresses
    - cdb_read.c: ``mmap(2)`` mode reading of DJB's CDB
    - humanize.c: Turn a large number into human readable string
    - freadline.c: Robust ``readline()`` that handles CR, LF
    - mkdirhier.c: C implementation of ``mkdir -p``
    - escape.cpp: Escape special chars in a string
    - unescape.cpp: Remove specially escaped chars
    - readpass.c: Portable C implementation to read password from
      terminal
    - parse-ip.c: Parse IPv4 address, address/mask combinaton
    - zbuf_c.c: Buffered I/O interface to Zlib compression
    - zbuf_unc.c: Buffered I/O interface to Zlib uncompress
    - error.c: Common function to print error string, ``errno`` and
      ``strerror(3)``.
    - uuid2str.c: Convert a UUID to printable string
    - rotatefile.cpp: Rotate a log file keeping the last "N" logs

BSD Licensed Code:

    - fts.c: Portable implementation of ``fts_open(3)`` and family 
    - ftw.c: Portable implementation of ``ftw(3)`` family of functions
    - getopt_long.c: Portable GNU ``getopt_long(3)``

