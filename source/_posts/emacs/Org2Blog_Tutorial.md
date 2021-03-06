---
title: Org to Wordpress with org2blog
categories: emacs
tags: emacs
date: 2017-05-25 19:58:42
---

# Publish with Org2Blog and Solution to non-ascii when posting to Wordpress

## Install packages

Install [org2blog](https://github.com/punchagan/org2blog). I put the package in my own emacs configuration folder. Path
to org2blog: **~/.spacemacs.d/layers/org2blog/**.

org2blog depends on

<!--more-->

1.  xml-rpc available at Launchpad [Launchpad](http://launchpad.net/xml-rpc-el)
2.  metaweblog.el available [here](https://github.com/punchagan/metaweblog)

To better manage the packages, I just put the two packages above right under the same path to my org2blog.

## Configuring Emacs

Put following code in your emacs configuration file, e.g. **~/.emacs.d/init.el**. Of course, change to your private
infomation, including my-blog, url, username. You need to put /xmlrpc.php after your url. That's for XML-RPC server of
your homepage. It only accepts POST request.

```commonlisp
;; Load your own org2blog path by using load-path.
(setq load-path (cons "~/.spacemacs.d/layers/org2blog/" load-path))
(require 'org2blog-autoloads)
(require 'auth-source) ;; or nothing if already in the load-path
(setq org2blog/wp-blog-alist
      '(("my-blog"
         :url "https://ztlevi.wordpress.com/xmlrpc.php"
         :username "ztlevi")))
(let (credentials)
  ;; only required if your auth file is not already in the list of auth-sources
  (add-to-list 'auth-sources "~/.netrc")
  (setq credentials (auth-source-user-and-password "wp-ztlevi"))
  (setq org2blog/wp-blog-alist
        `(("my-blog"
           :url "https://ztlevi.wordpress.com/xmlrpc.php"
           :username ,(car credentials)
           :password ,(cadr credentials)))))
```

Your **~/.netrc** file looks like this. Change the username and your<sub>password</sub> to your real ones.

`machine wp-ztlevi login username password your_password`

wp-ztlevi is the auth<sub>id</sub> to find your private information from the **~/.netrc** file.

## Useage

1.  _M-x org2blog/wp-new-entry_ : Create a new templete file.
2.  _M-x org2blog/wp-login_ : Login to your wordpress blog.
3.  _M-x org2blog/wp-post-buffer_ : Used to post your org file as draft.
4.  _M-x org2blog/wp-post-buffer-and-publish_ : Publish your org file right away.

## Solution to non-ascii on Wordpress

Since Wordpress does not support non-ascii when you post. We need to clear out the non-ascii characters before we post.
Otherwise it will failed with a structure problem like this.

<img src="https://ww3.sinaimg.cn/large/006tNc79gy1fdltj04hs4j307z06cq35.jpg" alt="img" title="image title"/>
So annoying when I first met this problem. I really had no ideas about this.

/Users/ztlevi/Dropbox/Beautify/OldWallPaper/001.jpg

```xml
<param>
  <value>
    <boolean>0</boolean>
  </value>
</param>
```

And Here is the **Solution**. Found in a Japanese blog :). <http://blog.somof.net/?p=1310>

测试是否能上传到 blog :)

I put some Chinese right here. Well, if you see the line above, that means it succeeds.

Add the following codes to your emacs configuration and you are good to go.

```commonlisp
(advice-add 'url-http-create-request :override
            'url-http-create-request-debug)
(defun url-http-create-request-debug (&optional ref-url)
  "Create an HTTP request for <code>url-http-target-url', referred to by REF-URL."
  (let* ((extra-headers)
         (request nil)
         (no-cache (cdr-safe (assoc "Pragma" url-http-extra-headers)))
         (using-proxy url-http-proxy)
         (proxy-auth (if (or (cdr-safe (assoc "Proxy-Authorization"
                                              url-http-extra-headers))
                             (not using-proxy))
                         nil
                       (let ((url-basic-auth-storage
                              'url-http-proxy-basic-auth-storage))
                         (url-get-authentication url-http-proxy nil 'any nil))))
         (real-fname (url-filename url-http-target-url))
         (host (url-http--encode-string (url-host url-http-target-url)))
         (auth (if (cdr-safe (assoc "Authorization" url-http-extra-headers))
                   nil
                 (url-get-authentication (or
                                          (and (boundp 'proxy-info)
                                               proxy-info)
                                          url-http-target-url) nil 'any nil))))
    (if (equal "" real-fname)
        (setq real-fname "/"))
    (setq no-cache (and no-cache (string-match "no-cache" no-cache)))
    (if auth
        (setq auth (concat "Authorization: " auth "\r\n")))
    (if proxy-auth
        (setq proxy-auth (concat "Proxy-Authorization: " proxy-auth "\r\n")))

    ;; Protection against stupid values in the referrer
    (if (and ref-url (stringp ref-url) (or (string= ref-url "file:nil")
                                           (string= ref-url "")))
        (setq ref-url nil))

    ;; We do not want to expose the referrer if the user is paranoid.
    (if (or (memq url-privacy-level '(low high paranoid))
            (and (listp url-privacy-level)
                 (memq 'lastloc url-privacy-level)))
        (setq ref-url nil))

    ;; url-http-extra-headers contains an assoc-list of
    ;; header/value pairs that we need to put into the request.
    (setq extra-headers (mapconcat
                         (lambda (x)
                           (concat (car x) ": " (cdr x)))
                         url-http-extra-headers "\r\n"))
    (if (not (equal extra-headers ""))
        (setq extra-headers (concat extra-headers "\r\n")))

    ;; This was done with a call to </code>format'.  Concatenating parts has
    ;; the advantage of keeping the parts of each header together and
    ;; allows us to elide null lines directly, at the cost of making
    ;; the layout less clear.
    (setq request
          (concat
             ;; The request
             (or url-http-method "GET") " "
             (url-http--encode-string
              (if using-proxy (url-recreate-url url-http-target-url) real-fname))
             " HTTP/" url-http-version "\r\n"
             ;; Version of MIME we speak
             "MIME-Version: 1.0\r\n"
             ;; (maybe) Try to keep the connection open
             "Connection: " (if (or using-proxy
                                    (not url-http-attempt-keepalives))
                                "close" "keep-alive") "\r\n"
                                ;; HTTP extensions we support
             (if url-extensions-header
                 (format
                  "Extension: %s\r\n" url-extensions-header))
             ;; Who we want to talk to
             (if (/= (url-port url-http-target-url)
                     (url-scheme-get-property
                      (url-type url-http-target-url) 'default-port))
                 (format
                  "Host: %s:%d\r\n" host (url-port url-http-target-url))
               (format "Host: %s\r\n" host))
             ;; Who its from
             (if url-personal-mail-address
                 (concat
                  "From: " url-personal-mail-address "\r\n"))
             ;; Encodings we understand
             (if (or url-mime-encoding-string
                     ;; MS-Windows loads zlib dynamically, so recheck
                     ;; in case they made it available since
                     ;; initialization in url-vars.el.
                     (and (eq 'system-type 'windows-nt)
                          (fboundp 'zlib-available-p)
                          (zlib-available-p)
                          (setq url-mime-encoding-string "gzip")))
                 (concat
                  "Accept-encoding: " url-mime-encoding-string "\r\n"))
             (if url-mime-charset-string
                 (concat
                  "Accept-charset: "
                  (url-http--encode-string url-mime-charset-string)
                  "\r\n"))
             ;; Languages we understand
             (if url-mime-language-string
                 (concat
                  "Accept-language: " url-mime-language-string "\r\n"))
             ;; Types we understand
             "Accept: " (or url-mime-accept-string "*/*") "\r\n"
             ;; User agent
             (url-http-user-agent-string)
             ;; Proxy Authorization
             proxy-auth
             ;; Authorization
             auth
             ;; Cookies
             (when (url-use-cookies url-http-target-url)
               (url-http--encode-string
                (url-cookie-generate-header-lines
                 host real-fname
                 (equal "https" (url-type url-http-target-url)))))
             ;; If-modified-since
             (if (and (not no-cache)
                      (member url-http-method '("GET" nil)))
                 (let ((tm (url-is-cached url-http-target-url)))
                   (if tm
                       (concat "If-modified-since: "
                               (url-get-normalized-date tm) "\r\n"))))
             ;; Whence we came
             (if ref-url (concat
                          "Referer: " ref-url "\r\n"))
             extra-headers
             ;; Length of data
             (if url-http-data
                 (concat
                  "Content-length: " (number-to-string
                                      (length url-http-data))
                  "\r\n"))
             ;; End request
             "\r\n"
             ;; Any data
             url-http-data))
    ;; Bug#23750
    ;;(unless (= (string-bytes request)
    ;;           (length request))
    ;;  (message "   text byte %d vs %d length" (string-bytes request) (length request)))
      ;;(message "===============================")
      ;;(error "Multibyte text in HTTP request: %s" request))
    (url-http-debug "Request is: \n%s" request)
    request))
```

BTW, you can add the function _occur-non-ascii_ to your emacs configuration. It will pop lines with non-ascii characters
in a buffer. Press **e** to edit.

```commonlisp
;; occur non ascii, used to check non-ascii in Wordpress
(defun occur-non-ascii ()
  "Find any non-ascii characters in the current buffer."
  (interactive)
  (push (if (region-active-p)
            (buffer-substring-no-properties
             (region-beginning)
             (region-end))
          (let ((sym (thing-at-point 'symbol)))
            (when (stringp sym)
              (regexp-quote sym))))
        regexp-history)
  (deactivate-mark)
  (occur "[^[:ascii:]]"))
```

If the highlight for the matches does not look so clear. Put the following line in your emacs custom setting for faces.
Change the background and foreground color to whatever you want.

```commonlisp
(custom-set-faces
 '(match ((t (:background "DeepSkyBlue1" :foreground "gray90" :weight bold))))
)
```
