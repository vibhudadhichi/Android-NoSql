# Android-NoSql

Lightweight, simple structured NoSQL database for Android

# Download

[ ![Download](https://api.bintray.com/packages/florent37/maven/android-nosql/images/download.svg) ](https://bintray.com/florent37/maven/android-nosql/_latestVersion)
```java
dependencies {
    compile 'com.github.florent37:android-nosql:1.0.0'
}
```

Save your datas as a structured tree

```java
noSql.put("/users/", "florent")
noSql.put("/users/", "kevin")
nosql.put("/identifiers/florent", 10)
nosql.put("/identifiers/kevin", 12)
```

The data structure will be

```java
/
---users/
      ---"florent"
      ---"kevin"
---identifiers/
      ---florent/
             ---10
      ---kevin/
             ---12
```

It'll be simple to search data

```java
int myId = noSql.get("/identifiers/florent/").integer();
```

# Serialize objects 

You can simply add nodes from POJOS

```java
final User user = new User(
                "flo",
                new House("paris"),
                Arrays.asList(new Car("chevrolet camaro"), new Car("ford gt"))
        );

noSql.put("/user/florent/", user);
```

```java
/
    users/
          florent/
                  name/
                       "flo"
                  house/
                        adress/
                               "paris"
                  cars/
                       0/
                         model/
                               "chevrolet camaro"
                       1/
                         model/
                               "ford gt"
```

# Get Objects from node
 
Or fetch nodes directly into Java Objects
 
```java
User user = noSql.get("/user/florent/", User.class);
```

# Initialisation

Android-NoSql need DataSavers to store your objets

```java
public class MainApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();

        AndroidNoSql.initWith(
                new SharedPreferencesDataSaver(getSharedPreferences("test", Context.MODE_PRIVATE))
        );
    }
}
```

It means you can store your data into SharedPreference, or SqlDatabase, or any storage library your want ;)

# Credits

Author: Florent Champigny [http://www.florentchampigny.com/](http://www.florentchampigny.com/)

Blog : [http://www.tutos-android-france.com/](http://www.www.tutos-android-france.com/)

<a href="https://plus.google.com/+florentchampigny">
  <img alt="Follow me on Google+"
       src="https://raw.githubusercontent.com/florent37/DaVinci/master/mobile/src/main/res/drawable-hdpi/gplus.png" />
</a>
<a href="https://twitter.com/florent_champ">
  <img alt="Follow me on Twitter"
       src="https://raw.githubusercontent.com/florent37/DaVinci/master/mobile/src/main/res/drawable-hdpi/twitter.png" />
</a>
<a href="https://www.linkedin.com/in/florentchampigny">
  <img alt="Follow me on LinkedIn"
       src="https://raw.githubusercontent.com/florent37/DaVinci/master/mobile/src/main/res/drawable-hdpi/linkedin.png" />
</a>


License
--------

    Copyright 2017 Florent37, Inc.

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
