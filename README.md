# RoverCore BreadCrumbs

This small library provides a service that makes it easy to add and customize breadcrumbs.  The idea is to allow you to create a simple list of breadcrumbs using this service that you can render using a component.  What's nice about this approach is that you can add the entire breadcrumb trail in an MVC action method and include the component in your shared _layout.cshtml page.

## Usage

### Install

Install the package using NuGet  
`Install-Package RoverCore.BreadCrumbs`

### Initialize

After you have setup your breadcrumbs you must add the breadcrumbs service:  
```cs
services.AddScoped<IBreadCrumbService, BreadCrumbService>();
```

### Adding breadcrumbs

Include the IBreadCrumbService dependency service in your controller. 

```cs 
public class DashboardController : Controller
{
  private readonly IBreadCrumbService _breadcrumbs;
  
  public HomeController (IBreadCrumbService breadcrumbs)
  {
    _breadcrumbs = breadcrumbs;
  }
  
  public IActionResult Index()
  {
    _breadcrumbs.StartAtAction("Dashboard", "Index", "Dashboard", new { Area = "Admin"})
        .Then("Home");
            
    return View();
  }

...
}

```

### Overriding the default look

Create a directory in your project at the path Views/Shared/Components/BreadCrumbs (in your views/shared folder create a Components subdirectory and then a BreadCrumbs subdirectory).  Copy the Views/Shared/Components/BreadCrumbs/Default.cshtml file from this project into that directory and customize how you wish.
