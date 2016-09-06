---
layout: post
title:  "Tenant-aware bean proxying"
date:   2013-06-21 12:57:00 +0200
categories: pustefix
---
In the last blog entry I showed how you can make Spring automatically create and manage an own bean instance per tenant using the tenant scope. Another use case within multitenant applications is using different beans (with different configuration or implementation, but common base class or interface) for different tenants.


Whereas the idea of the tenant scope is to inject a proxy object which delegates to an own bean instance of the same class (automatically managed for each tenant), now we inject a proxy object which delegates to other Spring managed beans (only needing a common interface or base class to be able to create a JDK proxy or CGLIB based proxy class).

With Spring's ProxyFactoryBean you can easily create AOP proxies. The AOP invocation target can be set using a TargetSource. Pustefix provides a custom TargetSource implementation, which returns the target bean for the currently set tenant.

Let's continue the Counter example from the last blog entry. We inject the counter bean into the web layer to increment the counter on each submit:

{% highlight java %}
  @Autowired Counter counter;

  public void handleSubmittedData(Context context, IWrapper wrapper) throws Exception {
    counter.increment();
  }
{% endhighlight %}

Now we want different Counter instances for different countries, but this time we also want different beans, having different implementation classes sharing a common Counter interface. Here you can see how the proxy bean is configured:

{% highlight xml %}
  <bean name="counter" class="org.springframework.aop.framework.ProxyFactoryBean">
    <property name="targetSource">
      <bean class="org.pustefixframework.container.spring.beans.TenantTargetSource">
        <property name="targets">
          <map>
            <entry key="DE">
              <bean class="mypackage.CounterImpl"/>
            </entry>
            <entry key="US">
              <bean class="mypackage.OtherCounterImpl"/>
            </entry>
          </map>
        </property>
      </bean>
    </property>
  </bean>
{% endhighlight %}

Pustefix also provide a custom ProxyFactoryBean implementation internally relying on the TenantTargetSource implementation, which makes the configuration a little bit shorter:

{% highlight xml %}
  <bean name="counter" class="org.pustefixframework.container.spring.beans.TenantProxyFactoryBean">
    <property name="targets">
      <map>
        <entry key="DE">
          <bean class="mypackage.CounterImpl"/>
        </entry>
        <entry key="US">
          <bean class="mypackage.OtherCounterImpl"/>
        </entry>
      </map>
    </property>
  </bean>
{% endhighlight %}

This feature will be available with Pustefix 0.18.48. 
