---
title: java中List的迭代删除
toc: true
date: 2019-06-26 16:33:22
category: java
tags: java
---

迭代器接口如下：

<!--more-->

```java
public interface Iterator<E> {
    boolean hasNext();
    E next();
    void remove();
}
```

java中List的迭代删除：

```java
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;
public class Test {

    public static void main(String[] args) {
        List<Person> list = new ArrayList<>();
        list.add(new Person(11));
        list.add(new Person(29));
        list.add(new Person(30));
        list.add(new Person(13));
        list.add(new Person(10));
      
        //迭代删除
        Iterator<Person> iterator = list.iterator();
        while (iterator.hasNext()) {
            Person person = iterator.next();
            if (person.getAge() > 15) {
                iterator.remove();  //这里注意是调用迭代器的remove方法
            }
        }
      
        System.out.println(list.toString());
    }

    public static class Person {
        private int age;

        public Person(int age) {
            this.age = age;
        }

        public int getAge() {
            return age;
        }

        public void setAge(int age) {
            this.age = age;
        }

        @Override
        public String toString() {
            return "[age=" + age + "]";
        }
    }
}
```

