Installation
============

Using pip:

* pip3 install markovgen --user

Or

From the git repository:

* git clone https://github.com/ProgVal/markovgen.git
* cd markovgen
* python3 setup.py install --user


Command-line usage
==================

Usage:
    python3 -m markovgen <extracter> <path to log file>

Supported extracters are:

* srt
* supybot
* weechat
* xchat
* plain



Usage as a library
==================

markovgen.Markov:
    __init__(messages=[]):
        takes an optional list of initial messages.

    feed(message):
        takes a message and adds it to the cache.

    feed_from_file(file_descriptor, extracter):
        Reads the file descriptor line by line, apply the extracter to
        it, and feeds the cache with the return value of the extracter.

    generate_markov_text(max_size=30, seed=None, backward=False):
        Generate a text based on the cache.
        Selects a random word in the cache as the first (resp. last) word,
        and continues forward (resp. backward) using the cache in the
        right direction, until it selects a message end from the cache
        or that the max_size is met.
        The seed may be a string or a 2-tuple of strings.

    available_seeds(backward=False):
        Returns a view on the 2-tuples of words in the corpus.
        Useful if you want to match them against a new message.

@mixed_encoding_extracting:
    decorator for extracters that handle decoding messages with the
    right charset (if chardet or charade is installed) or as utf8
    (otherwise)
