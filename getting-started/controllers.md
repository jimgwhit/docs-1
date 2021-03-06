Controllers are the bread and butter of the framework they control when a model is used and equally when to include a view for output. A controller is a class with methods, these methods are the outputted pages when used in conjunction with routes.

A method can be used for telling a view to show a page or outputting a data stream such as XML or a JSON array. Put simply they are the logic behind your application.

Controllers can be placed in subfolders relative to the root of the Controllers folder, each class located in subfolders must have its own namespace, for instance a subfolder called Admin and a class called Users should have a namespace of **App\Controllers\Admin**

Controllers are created inside the **app/Controllers** folder. To create a controller, create a new file, the convention is to **StudlyCaps** without any special characters or spaces. Each word of the filename should start with a capital letter. For instance: **AddOns.php**.

Controllers will always use a namespace of **App\Controllers**, if the file is directly located inside the controllers folder. If the file is in another folder that folder name should be part of the namespace.

For instance, a controller called Blog located in **app/Controllers/Blog** would have a namespace of **App\Controllers\Blog**

Controllers can extend from the base controller located in **app/Controllers/BaseController.php**  the syntax is:

```php
namespace App\Controllers;

use App\Controllers\BaseController;

class Posts extends BaseController 
{

}
```

Also, the view class is needed to include view files, you can call the namespace then the view:

Create an alias:

```php
use Nova\Support\Facades\View;
```

Then to use:

```php
return View::make('path')->shares('title', 'Welcome');
```

**Example**

```php

namespace App\Controllers;

use App\Controllers\BaseController;
use Nova\Support\Facades\View;

class Posts extends BaseController
{
    public function index()
    {   
        return View::make('Posts/Index')->shares('title', 'Posts');
    }
}
```


Models can be used in a constructor and added to a property then becoming available to all methods. The model will need to use its namespace while being called

```php
namespace App\Controllers;

use App\Controllers\BaseController;
use App\Models\Post;
use Nova\Support\Facades\View;

class Posts extends BaseController 
{
    private $post;

    public function __construct()
    {
        parent::__construct();
        $this->post = new Post();
    }

    public function index()
    {
        $posts = $this->post->getPosts();
        View::make('Blog/Posts')->shares('title', 'Blog')->with('posts', $posts);
    }
}
```

### Methods

A controller can have many methods, a method can call another method, all standard OOP behaviour is honoured. Data can be passed from a controller to a view by passing an array to the view. The array can be made up from keys. Each key can hold a single value or another array. The array must be passed to the method for it to be used inside the view page or in a template (covered in the templates section)

```php
$content = 'The contacts for the page';
$users = array('Dave', 'Kerry', 'John');

return View::make('Contacts', compact('content', 'users');
```
