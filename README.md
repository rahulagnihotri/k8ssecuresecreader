# k8ssecuresecreader
<b>Quick alternative of unmounting secrets in kubernetes </b>.

Secrets can be mounted as data volumes . Inside the container secrets are mounted at a directory in plain text.
If your pod allows getting into a shell or ssh into othe pod , it becomes imperative that these secrets are not present in fileystem.<br><br>
There are many other ways example using vault for fetching secrets , But this is one way where in you can mount them as volume and use init containers and shared volumes  to remove the secrets post use . As of now there is no direct  way in kubernetes to unmount secret 
<br>https://github.com/kubernetes/kubernetes/issues/41193<br><br>
<b> Basic flow:</b><br>
1.Create an init container with shared volume with the main container<br>
2. The init container acts as a secret injector and copies the secret to shared path<br>
3. The main pod acts as a secret reader from shared pod and then post reading deletes the secrets from the directory
