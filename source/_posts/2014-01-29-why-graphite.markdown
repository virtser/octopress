---
layout: post
title: "Why Graphite"
date: 2014-02-04 20:58
comments: true
published: false
---
![](http://graphite.wdfiles.com/local--files/screen-shots/graphite_fullscreen_800.png)

There are many posts in the Internet about what is [Graphite](http://graphite.wikidot.com/) and how to work with it. In this post I want to talk about why any professional engineer (developer) have to work with Graphite.

During my Graphite implementation sessions with engineers in [eToro](http://www.etoro.com/) I felt difficulty to explain developers what is Graphite and why they want to use it instead (or in addition to) other monitoring tools.

We tried variety of different logging and monitoring tools in eToro in the last year. We are using log4net to save our logs in files. We used to work with [LogEntries](https://logentries.com/) to store our logs in cloud, but we decided that it doesn't precisely fit our needs and now we almost finished the migration to [Splunk](http://www.splunk.com/). Splunk knows to do logs analysis better in addition to aggregations, correlations and dashboards. 

We also working with [New Relic](http://newrelic.com/) which is really simple to install. You just need to install an agent on your web server and you get a great visibility on your application performance including database and external dependencies. But we faced few problems with it. Most of our applications are written in .NET and some types of applications like WCF, Web API or [ServiceStack](https://servicestack.net/) API were not well supported by New Relic (could be that they added a better support by now) and returned wrong numbers if at all. In addition we found in some unknown cases that New Relic agent installed on IIS caused sometimes to random application pool restarts.

And now before I explain why Graphite, I have to explain in short about what is Graphite. Roughly Graphite is a metrics collector. You can report withing the code of your application counts, timers and gauges. You can count how many times some method in your application was called or the time it took to execute this method. You give your metric a name separated by dots and Graphite knows to break it and show it as a tree in its UI (see the screenshot above).

<!-- more -->

For example, you can count successful user sign ups by adding the following line in your code where you are sure that the sign up completed:

`StatsdClient.Metrics.Counter("eToro.SignUp.Success");`

or failed:

`StatsdClient.Metrics.Counter("eToro.SignUp.Failure");`

or measure the latency of sign up method:

`StatsdClient.Metrics.Timer("eToro.SignUp", elapsedTime);`

By the way, timers includes counters as well. You don't have to count the call again if you time it.

* In this example I'm using [StatsD C# Client](https://github.com/goncalopereira/statsd-csharp-client)

StatsD is a client which received the metrics by UDP, process it, applies some math function and stores it in Graphite. (this in not 100% correct, I wrote it as I wrote in terms of simplicity)

So now, when you have some high level clue about what you can do with Graphite, we will talk why we (as developers) have to use Graphite.

**Graphite advantages:**

1. Once Graphite and StatsD servers are installed and all the required ports are open in firewall to accept UPD connections it requires absolutely no IT intervention, but only for regular daily monitoring and maintenance of up time. I mean that we, as developers, are completely independently can add new metrics to our code and they will appear in Graphite when you deploy the application to production.

2. Graphite just gives power to developers. We control where to place our metrics, how do they behave and how we build our graphs based on these metrics. In case of New Relic, it is a black box, you never know when do they start to measure some metric and when do they stop. In case of Graphite you know exactly where to start measuring time and where to stop it, it gives you depth. We also have full control on the name of the metrics. You can include withing the code scope to metric name some dynamic parameters like "machine name" for example.

3. Graphite is non blocking. You report your metrics over UDP which is non blocking protocol. You can do in synchronously in your code and even if Graphite server is not responding, your application will work as usual.

4. Graphite knows to smartly aggregate your data and shrink it over time. You can define it for example to keep every second of data in the first week, then every minute in the first month, then every date in the first year. This way you don't have to keep tons of metrics, but you know exactly the file size of each metric.

5. Graphite is very easy to work with. After reporting a metric, it is a matter of one click on that metric and you can see your metric graph. You can easily drop one graph to another to merge them and see in one window. You can apply math functions on your graphs and save multiple graph windows as dashboards. And more...

Ofcourse you can report counters and timers to your logs and then ask Splunk to collect the logs, process them and build some nice dashboards, but why? If you have like millions of lets say impressions or click you need to count? It make no sense to flood your logs with data which you want to see as graph. Logs are meant to keep your errors and debug info if required, keep them as clean as possible, otherwise it will be hard to analyse.

With Graphite you should measure every method in your application and all your external dependencies like database calls, cache hit/miss, messaging. Its up to you and your application business logic.

Another code example where we created a custom .NET [*GraphiteTiming*] attribute using  [PostSharp](http://www.postsharp.net/) library in order to do quick metrics instumentation of each method in a class (if you set the attribute on class level) to measure time (and number of executions) in addition to counting the exceptions:


    [Serializable]
    public sealed class GraphiteTimingAttribute : OnMethodBoundaryAspect
    {
        [NonSerialized]
        private Stopwatch _stopwatch;
        
        public override void OnEntry(MethodExecutionArgs args)
        {
            _stopwatch = Stopwatch.StartNew();
            base.OnEntry(args);
        }

        public override void OnExit(MethodExecutionArgs args)
        {
                StatsdClient.Metrics.Timer(
                    string.Format("{0}.{1}.{2}.{3}", 
                    "ApplicationName", 
                    System.Environment.MachineName, 
                    args.Method.DeclaringType.Name, 
                    args.Method.Name), 
                    (int)_stopwatch.Elapsed.TotalMilliseconds
                );
            base.OnExit(args);
        }

        public override void OnException(MethodExecutionArgs args)
        {
            StatsdClient.Metrics.Counter(
            	string.Format("{0}.{1}.error",
            	args.Method.DeclaringType.Name,
            	args.Method.Name),
            	(int)_stopwatch.Elapsed.TotalMilliseconds);
            base.OnException(args);
        }
    }


If you didn't try Graphite yet, you should definitely do! it gives you "eyes" to see what is happening with your application in real time. 

Like some wise man said, life of a good developer splits to two - before Graphite and after Graphite. ;)


Must read references to Graphite information:

* [Measure Anything, Measure Everything](http://codeascraft.com/2011/02/15/measure-anything-measure-everything/)
* [Practical Guide to StatsD/Graphite Monitoring](http://matt.aimonetti.net/posts/2013/06/26/practical-guide-to-graphite-monitoring/)
* [Understanding StatsD and Graphite](http://blog.pkhamre.com/2012/07/24/understanding-statsd-and-graphite/)
* [Span vs Median for Response Time Monitors](http://steveakers.com/2013/08/01/span-vs-median-for-response-time-monitors/)
* [10 Things I Learned Deploying Graphite](http://kevinmccarthy.org/blog/2013/07/18/10-things-i-learned-deploying-graphite/)