# Security First Website
This is the repository of Security First website. 
The current online version of this portal can be found at https://secfirst.org.

## Compiling a local version of the website

1. Install [Hugo](https://gohugo.io/getting-started/installing/).

2. Create a new Hugo site and enter into the site folder:
    ```
    hugo new site secfirst
    cd secfirst
    ```
3. Clone the secfirst.org website inside your Hugo site folder:

    ```
    $ git clone https://github.com/securityfirst/secfirst.org.git
    ```
4. Enter the secfirst.org directory and start the Hugo server:
    ```
    cd secfirst.org
    hugo server -D
    ```
    You should be able to access your local instance at http://localhost:1313/.
