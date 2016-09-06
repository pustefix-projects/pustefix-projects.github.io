---
layout: post
title:  "Multitenant Spring beans in Pustefix"
date:   2013-04-09 16:40:00 +0200
categories: pustefix
---
Pustefix's multitenancy support lets you create applications serving multiple tenants (e.g. countries) and languages within a single application instance. So far multitenancy in Pustefix focused on the view layer, helping you create internationalized pages composed of tenant/language-dependent content and resources.

In the next step we want to extend Pustefix's application logic layer with multitenant capabilities. Looking at a usual Pustefix application's Spring configuration we normally see a lot of singleton scoped beans implemented with a concrete application instance in mind. Making such an application multitenant means that such a bean will be shared between the tenants. Imagine a simple counter bean backing a website request counter. It will count the total number of requests, independent of the tenant. But what, if you want to have an own counter for each supported tenant?

You could create multiple counter beans, manage them in a map keyed by the tenant name and programmatically select the according counter within the request processing logic. But wouldn't it be much nicer, if you don't have to care about the tenants in your code and let Spring automatically manage this for you?

The solution is the implementation of an own tenant-aware Spring scope. Giving a Spring bean tenant scope, will mean that an own instance of this bean will be created and managed for each tenant. Injecting the bean as dependency will work similar to session-scoped beans: Spring will inject a proxy bean, which will delegate method calls to the appropriate instance associated with the current tenant.

A bean can be made tenant-scoped by setting the according scope attribute within the Spring configuration:

{% highlight xml %}
  <bean name="counter" class="mypackage.Counter" scope="tenant">
    <aop:scoped-proxy/>
  </bean>
{% endhighlight %}

Using the bean, e.g. in an IHandler, is straightforward:

{% highlight java %}
  @Autowired Counter counter;

  public void handleSubmittedData(Context context, IWrapper wrapper) throws Exception {
    counter.increment();
  }
{% endhighlight %}

This feature will be available with Pustefix 0.18.44. 

The next step will be the transparent injection of different tenant-depending bean instances (e.g. differently configured instances of the same class or different implementations of a common interface) using Spring's ProxyFactoryBean together with a tenant-aware TargetSource implementation. 
 
