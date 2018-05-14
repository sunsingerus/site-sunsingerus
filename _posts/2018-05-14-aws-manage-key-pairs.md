---
ID: 446
post_title: AWS. Manage Key Pairs
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/aws-manage-key-pairs/
published: true
post_date: 2018-05-14 11:05:20
---
<h1>Create New Key Pair</h1>

Open <code>Services -> EC2</code>
On the left side menu select <code>Key Pairs</code> and then click <code>Create Key Pair</code>
<img src="https://sunsingerus.com/wp-content/uploads/2018/05/1_create_key_pair.png" alt="" width="483" height="183" class="alignnone size-full wp-image-447" />
Let's call it <code>ubuntu_key_pair</code> and click <code>Create</code>
Download <code>.pem</code> file
<img src="https://sunsingerus.com/wp-content/uploads/2018/05/2_download_pem_file.png" alt="" width="500" height="500" class="alignnone size-full wp-image-448" />
which is a private key, with the following content
<pre>
-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEAqgJJItUsUicOuTeW9PoCRxYetS63e5Qh4Ee18Y6lx+zoWT0EIF3HYdJvdZR+
...
bj84nUsk2odCOD3+pGjzGaX13U0o4kCi+Pm0CBf342ICqyvDpnmOkEiH7adS1qxZdZE0
-----END RSA PRIVATE KEY-----
</pre>