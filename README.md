
#### Add Some Content

    $ hugo new posts/my-first-post.md
    
Edit the newly created content file if you want. Now, start the Hugo server with drafts enabled:    

    $ hugo server -D
    
#### Deploy

    $ hugo
    $ git add --all && git commit -m "Publishing to gh-pages"
    
Mail document is basically `docs`.