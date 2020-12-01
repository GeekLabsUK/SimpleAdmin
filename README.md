# SimpleAdmin
Codeigniter 4 Boilerplate Admin Dashboard, built on the backbone of SimpleAuth

### Folder Structure
In order to keep SimpleAdmin clean and modular all roles, users, modules and expantions will all have their own dedicated folder structure. I.e :

```
|--App
|  |--Controlers
|     |--Admin (our main route for all admin role controllers)
|        |--> AdminAuthController.php
|        |--Modules (Our modules folder for additional addon modules
```

### Creating A New Role Type
We can add as many different role types as we like. Roles should be thought of as top level permissions or departments. Such as a SuperAdmin, Admin, Customer, Staff etc. Each role type will have its own dedicated controller, model and DB table.

## Create an 'Admin' User
In order for us to build out our dashboard we need levels of access, in this example we will build an 'Admin' section. This will need a Controller, A Model and a DB table to handle our 'Admin' users. SimpleAdmin has been designed to be easy to build your next application, The majority of the tutorials and examples are written with begginers in mind.

## Create the Controller
The first thing we need to do is start building our controller that will handle all of our authentication, Registrations, Logins etc. SimpleAuth is the backbone of SimpleAdmin and the library will handle almost all of our auth requirements.

Lets create our folder structure. Create a new folder named 'Admin' in our App\Controllers directory and create a new file named **AdminAuthController.php**

We are now working inside a subdirectory of our Controllers folder so we need to set our namespace to reflect this. We will also need to to include our BaseControler and the SimpleAuth library. Name the class' AdminAuthController'. We will create a __construct function and assign our auth library so it can be used throughout all of our controllers methods.

```php
 namespace App\Controllers\Admin;

 use \App\Controllers\BaseController; // Include BaseController
 use \App\Libraries\AuthLibrary; // Include AuthLibrary

class AdminAuthController extends BaseController
{
	public function __construct()
	{
		
		$this->Auth = new AuthLibrary;
		
	}
```

Now we can interact with the librarys classes by using **$this->Auth**

Lets create our index method

```php
public function index()
	{

	 return redirect()->to($this->Auth->autoRedirect());	
		
	}
```

As you can see we have included our first call to the AuthLibrary **$this->Auth->autoRedirect()** SimpleAuth uses auto redirects and will dynamically redirect users based on their roles. In order for this to work we first need to set up our roles and redirect routes in the AuthConfig.php config file located in the App\Config folder.

For this example we will be building out the Admin user role as our top level access but for future expansion we are also going to assign a SuperAdmin role. The roles are saved in the **$assignRoles** array. Set the SuperAdmin role to '1' and the Admin role to '2'. Everything we do from now on will reference the integers we have assigned here. Any interger can be passed and as many different roles as needed can be declared. 

```php
public $assignRoles = [
        'SuperAdmin' => '1',
        'Admin' => '2',        
    ];
```

We can now declare the default redirect route we will be using for that role. 

```php
public $assignRedirect = [
        '1' => '/superadmin',
        '2' => '/dashboard',        
    ];
```

There is no need for a user to access the index method of our controller, we could either not declare it at all or we can use our auto redirect **$this->Auth->autoRedirect()** The user will get redirected to /dashboard if they are an Admin or role '2'. This is the most simple use of the dynamic auto redirect system built into SimpleAuth but becomes alot more powerfull when auto redirecting form submitions, registrations etc.

Why dont we just not declare the index method? Honestly its probably just developer preference but we believe if a user is following routes to methods in that controller such as Auth/Login or Auth/Register the user could try to navigate to Auth directly, if we have no index method we get a 404 error. 404 errors look bad so instead lets redirect them. 

## Controller Methods

We now need to decide what methods we need to include in our controller, and what methods of the AuthLibrary class we need to use. The most simplest would be login and logout methods. Do we require user registration? Do we want to offer forgot password functionality or remember me? Do we want to use a lock screen? For this example we will include the full functionality of SimpleAuth so we will start by registering a user.

Create a new method named register()

```php
public function register()
	{
		
	}
```



