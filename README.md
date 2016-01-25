OhmDB
=====

> OhmDB is "the irresistible database" that offers the power of relational databases and the flexibility of NoSQL databases.

[![Maven Central](http://img.shields.io/maven-central/v/com.gitblit.ohmdb/ohmdb.svg)](http://search.maven.org/#search|ga|1|com.gitblit.ohmdb)
[![Maven Central](https://img.shields.io/github/license/gitblit/ohmdb.svg)](http://www.apache.org/licenses/LICENSE-2.0.txt)

## Fork

OhmDB is a great tool to persist, retrieve, and query objects from disk.  Whether it lives up to the above blockquote written by the original author is for you to decide.

This fork of OhmDB makes some modest changes including...

1. Requiring Java 8
2. Improved support for nested POJO fields persisted in your tables
3. Ensures strings are encoded and decoded as UTF8 instead of the system encoding.

While the API remains unchanged, the change to the string encoding **may** not be compatible with existing OhmDB 1.0.0 files. YMMV.

## Apache Public License v2

OhmDB is released under the liberal APL v2 license, so it is free to use for both commercial and non-commercial projects.

## Using with Maven

Add the following snippet to the `<dependencies>` section in pom.xml:

```xml
<dependency>
    <groupId>com.gitblit.ohmdb</groupId>
    <artifactId>ohmdb</artifactId>
    <version>1.0.1</version>
</dependency>
```

## Quick start

* Add the `ohmdb` dependency to your Maven project (as described above).

* Add the following code to your project, and execute it:
 
```java
import com.ohmdb.api.*;

class Person { public String name; public int age; }

public class Main {
	public static void main(String[] args) {
		Db db = Ohm.db("ohm.db");
		Table<Person> persons = db.table(Person.class);
		Person $p = persons.queryHelper();

		Person p1 = new Person();
		p1.name = "Niko";
		p1.age = 30;
		long id = persons.insert(p1);
		Person p2 = persons.get(id);

		persons.createIndexOn($p.age);
		Person[] adults = persons.where($p.age).gte(18).get();
      
        db.shutdown();
	}
}
```

## Features

* Simple setup, no configuration (just add it as Maven dependency, and you are ready!)

* Delightful API:

```java
Ohm.db("ohm.db").table(Item.class).insert(new Item("item1"));
``` 

or just:

```java
DB.insert(new Item("item1"));
```

* ACID transactions with automatic recovery

* Fast joins through graph-based relations with graph traversal optimization 

* Automatic schema migration

* Single-file storage (e.g. my.db), so "backup" == "copy the file!"

## Contributing

1. Fork (and then `git clone https://github.com/gitblit/ohmdb.git`).
2. Create a branch (`git checkout -b branch_name`).
3. Commit your changes (`git commit -am "Description of contribution"`).
4. Push to the branch (`git push origin branch_name`).
5. Open a Pull Request.
6. Thank you for your contribution! Wait for a response...
