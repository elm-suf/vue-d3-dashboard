<template>
  <div id="about">
    <v-app id="app-about">
      <v-container fluid grid-list-sm>
        <v-content>
        <h1>Hits Algorithm</h1>
          <p>
           <strong>Hyperlink-Induced Topic Search</strong>  (HITS; also known as hubs and authorities) is a link analysis algorithm that rates Web pages, developed by Jon Kleinberg.<br>
            The idea behind Hubs and Authorities stemmed from a particular insight into the creation of web pages when the Internet was originally forming; that is, certain web pages, known as hubs, served as large directories that were not actually authoritative in the information that they held, but were used as compilations of a broad catalog of information that led users direct to other authoritative pages. In other words, a good hub represented a page that pointed to many other pages, and a good authority represented a page that was linked by many different hubs.
            <br>
            The scheme therefore assigns two scores for each page: its authority, which estimates the value of the content of the page, and its hub value, which estimates the value of its links to other pages.
          </p>
          <hr>

          <v-card>
            <v-card-title>Pseudocode</v-card-title>
            <v-card-text>
              <code>
                1 G := set of pages
                2 for each page p in G do
                3   p.auth = 1 // p.auth is the authority score of the page p
                4   p.hub = 1 // p.hub is the hub score of the page p
                5 function HubsAndAuthorities(G)
                6   for step from 1 to k do // run the algorithm for k steps
                7     norm = 0
                8     for each page p in G do  // update all authority values first
                9       p.auth = 0
                10       for each page q in p.incomingNeighbors do // p.incomingNeighbors is the set of pages that link to p
                11          p.auth += q.hub
                12       norm += square(p.auth) // calculate the sum of the squared auth values to normalise
                13     norm = sqrt(norm)
                14     for each page p in G do  // update the auth scores
                15       p.auth = p.auth / norm  // normalise the auth values
                16     norm = 0
                17     for each page p in G do  // then update all hub values
                18       p.hub = 0
                19       for each page r in p.outgoingNeighbors do // p.outgoingNeighbors is the set of pages that p links to
                20         p.hub += r.auth
                21       norm += square(p.hub) // calculate the sum of the squared hub values to normalise
                22     norm = sqrt(norm)
                23     for each page p in G do  // then update all hub values
                24       p.hub = p.hub / norm   // normalise the hub values
              </code>
            </v-card-text>
          </v-card>

          <v-card>

          </v-card>
        </v-content>

      </v-container>
    </v-app>
  </div>
</template>
