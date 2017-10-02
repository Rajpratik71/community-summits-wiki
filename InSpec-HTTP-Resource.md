-- I shell out to curl, and then try to parse that versus regex, because the HTTP call doesn't work on remote machines. 

- I'm sorry, it should work on local and remote. 2 resources with this issue SSL/HTTP. We don't alter the state of the machine to run InSpec. The way to fix this is to wrap curl, it hasn't been fixed besides time. We should fix this during hack day.

-- How about windows...

- Let's start here, we'll make it optimal for 2.0. If host has no curl, make the end user responsible to installing curl. We want the UX to be the same for local and remote. Platform RFC will be able to flag a resource for platform support. We skip resource for lack of OS support.

- Let's push a remote http 1.0, make sure it works. What we need to expose: status code, headers as a hash and the content. We can expand to HTTPS, with disabled SSL cert.



