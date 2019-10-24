# NetCore-RobotsMiddleware
Sample code for NetCore middleware for blocking bots from crawling your site over a given domain name (i.e. *.azurewebsites.net*). It works by overriding your **robots.txt** response when it is loaded over a given domain and it returns:
```
User-agent: *
Disallow: /
```

## Usage
1. Add the **RobotsMiddleware.cs** to your project. 
2. Set the domain that you want to return `Disallow: /`
3. Register your middleware in your **Startup.cs** file.
```
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
      ...
      //custom middleware defined in this website code
			app.MapWhen(context => context.Request.Path.Value.EndsWith("robots.txt", true, null),
						appBranch => { appBranch.UseRobotsHandler(); });
      ...
}
```

## Test
Run the site over the domain you want to `Disallow: /` by making a request to `https://{your-site}/robots.txt` and you should see this response:
```
User-agent: *
Disallow: /
```
