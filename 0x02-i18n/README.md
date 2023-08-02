130
131
132
133
134
135
136
137
138
139
140
141
142
143
144
145
146
147
148
149
150
151
152
153
154
155
156
157
158
159
160
161
162
163
164
165
166
167
168
169
170
171
172
173
174
175
176
177
178
179
180
181
182
183
184
185
186
187

-   GitHub repository: `alx-backend`
-   Directory: `0x02-i18n`
-   File: `3-app.py, babel.cfg, templates/3-index.html, translations/en/LC_MESSAGES/messages.po, translations/fr/LC_MESSAGES/messages.po, translations/en/LC_MESSAGES/messages.mo, translations/fr/LC_MESSAGES/messages.mo`



### 4\. Force locale with URL parameter

In this task, you will implement a way to force a particular locale by passing the `locale=fr` parameter to your app's URLs.

In your `get_locale` function, detect if the incoming request contains `locale` argument and ifs value is a supported locale, return it. If not or if the parameter is not present, resort to the previous default behavior.

Now you should be able to test different translations by visiting `http://127.0.0.1:5000?locale=[fr|en]`.

**Visiting `http://127.0.0.1:5000/?locale=fr` should display this level 1 heading:** ![](https://s3.amazonaws.com/alx-intranet.hbtn.io/uploads/medias/2020/3/f958f4a1529b535027ce.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIARDDGGGOUSBVO6H7D%2F20220719%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20220719T232414Z&X-Amz-Expires=86400&X-Amz-SignedHeaders=host&X-Amz-Signature=9b67dd8c671452469476255ea5d70325bb8a073061b5b0b924973219f33823f6)

**Repo:**
-   GitHub repository: `alx-backend`
-   Directory: `0x02-i18n`
-   File: `4-app.py, templates/4-index.html`



### 5\. Mock logging in

Creating a user login system is outside the scope of this project. To emulate a similar behavior, copy the following user table in `5-app.py`.

```
users = {
    1: {"name": "Balou", "locale": "fr", "timezone": "Europe/Paris"},
    2: {"name": "Beyonce", "locale": "en", "timezone": "US/Central"},
    3: {"name": "Spock", "locale": "kg", "timezone": "Vulcan"},
    4: {"name": "Teletubby", "locale": None, "timezone": "Europe/London"},
}
```

This will mock a database user table. Logging in will be mocked by passing `login_as` URL parameter containing the user ID to log in as.

Define a `get_user` function that returns a user dictionary or `None` if the ID cannot be found or if `login_as` was not passed.

Define a `before_request` function and use the `app.before_request` decorator to make it be executed before all other functions. `before_request` should use `get_user` to find a user if any, and set it as a global on `flask.g.user`.

In your HTML template, if a user is logged in, in a paragraph tag, display a welcome message otherwise display a default message as shown in the table below.

| msgid | English | French |
| `logged_in_as` | `"You are logged in as %(username)s."` | `"Vous êtes connecté en tant que %(username)s."` |
| `not_logged_in` | `"You are not logged in."` | `"Vous n'êtes pas connecté."` |

**Visiting `http://127.0.0.1:5000/` in your browser should display this:**

![](https://s3.amazonaws.com/alx-intranet.hbtn.io/uploads/medias/2020/3/2c5b2c8190f88c6b4668.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIARDDGGGOUSBVO6H7D%2F20220719%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20220719T232414Z&X-Amz-Expires=86400&X-Amz-SignedHeaders=host&X-Amz-Signature=58edc296f4010cf9bfbfad1a6669eeaa6a98b680439961e01f247fa3ac924c19)

**Visiting `http://127.0.0.1:5000/?login_as=2` in your browser should display this:** ![](https://s3.amazonaws.com/alx-intranet.hbtn.io/uploads/medias/2020/3/277f24308c856a09908c.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIARDDGGGOUSBVO6H7D%2F20220719%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20220719T232414Z&X-Amz-Expires=86400&X-Amz-SignedHeaders=host&X-Amz-Signature=bb18ed9baad90f89a6fa63543b018f6d809d4373c41c1577a663307f470e6076)

**Repo:**
-   GitHub repository: `alx-backend`
-   Directory: `0x02-i18n`
-   File: `5-app.py, templates/5-index.html`

