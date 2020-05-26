---
title: Iterating complex data structure
date: 2020-05-24 03:29:22
tags:
---

Let say we have an array of authors
<pre>

const myFavouriteAuthors = [
  'Neal Stephenson',
  'Arthur Clarke',
  'Isaac Asimov', 
  'Robert Heinlein'
];
</pre>
we can iterate all authors using any loop or for of here, but if we modify the data structure in below format,
<pre>

const myFavouriteAuthors = {
  allAuthors: {
    fiction: [
      'Agatha Christie', 
      'J. K. Rowling',
      'Dr. Seuss'
    ],
    scienceFiction: [
      'Neal Stephenson',
      'Arthur Clarke',
      'Isaac Asimov', 
      'Robert Heinlein'
    ],
    fantasy: [
      'J. R. R. Tolkien',
      'J. K. Rowling',
      'Terry Pratchett'
    ],
  }
}
</pre>
then you cannot iterate all authors using for loop or any other loop with ease. So we can write our own method 
<pre>

const myFavouriteAuthors = {
  allAuthors: {
    ...
  },
  getAllAuthors() {
  	const authors = [];

  	for (const author of this.allAuthors.fiction) {
  		authors.push(author);
  	}

  	for (const author of this.allAuthros.scienceFiction) {
  		authors.push(author);
  	}

  	for (const author of this.allAuthors.fantasy) {
  		authors.push(author);
  	}

  	return authors;
  }
}
</pre>
The problem with this approrach is we need to be aware of the method called getAllAuthors and if our data sctructure has one more genre then we need to modify the getAllAuthors function as well. This is not cool.

So, what's the other approach is make our data structure iterable. Can we do that. Yes we can!!

An iterable is a data structure that wants to make its elements accessible to the public. It does so by implementing a method whose key is Symbol.iterator. That method is a factory for iterators. That is,  it will create iterators.

<pre>
const myFavouriteAuthors = {
  allAuthors: {
    fiction: [
      'Agatha Christie', 
      'J. K. Rowling',
      'Dr. Seuss'
    ],
    scienceFiction: [
      'Neal Stephenson',
      'Arthur Clarke',
      'Isaac Asimov', 
      'Robert Heinlein'
    ],
    fantasy: [
      'J. R. R. Tolkien',
      'J. K. Rowling',
      'Terry Pratchett'
    ],
  },
  [Symbol.iterator]() {
    // Get all the authors in an array
    const genres = Object.values(this.allAuthors);
    
    // Store the current genre and author index
    let currentAuthorIndex = 0;
    let currentGenreIndex = 0;
    
    return {
      // Implementation of next()
      next() {
        // authors according to current genre index
        const authors = genres[currentGenreIndex];
        
        // doNotHaveMoreAuthors is true when the authors array is exhausted.
        // That is, all items are consumed.
        const doNothaveMoreAuthors = !(currentAuthorIndex < authors.length);
        if (doNothaveMoreAuthors) {
          // When that happens, we move the genre index to the next genre
          currentGenreIndex++;
          // and reset the author index to 0 again to get new set of authors
          currentAuthorIndex = 0;
        }
        
        // if all genres are over, then we need tell the iterator that we 
        // can not give more values.
        const doNotHaveMoreGenres = !(currentGenreIndex < genres.length);
        if (doNotHaveMoreGenres) {
          // Hence, we return done as true.
          return {
            value: undefined,
            done: true
          };
        }
        
        // if everything is correct, return the author from the 
        // current genre and incerement the currentAuthorindex
        // so next time, the next author can be returned.
        return {
          value: genres[currentGenreIndex][currentAuthorIndex++],
          done: false
        }
      }
    };
  }
};

for (const author of myFavouriteAuthors) {
  console.log(author);
}

console.log(...myFavouriteAuthors)
</pre>