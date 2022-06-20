##### Project 

# Authentication
#### Installing breze 

Laravel Breeze is a minimal, simple implementation of all of Laravel's authentication features, including login, registration, password reset, email verification, and password confirmation. Laravel Breeze's default view layer is made up of simple Blade templates styled with Tailwind CSS.

1. install via composer

    `composer require laravel/breeze --dev`

2. Install breeze scafolding :
    This command publishes the authentication views, routes, controllers, and other resources to your application. Laravel Breeze publishes all of its code to your application so that you have full control and visibility over its features and implementation. After Breeze is installed, you should also compile your assets so that your application's CSS file is available:

    `php artisan breeze:install`

3. now `npm install && npm run dev`

4. finally run `php artisan migrate`

now we can register an account , login 
we can reset passwords , the forget password functionality is also built-in

# verfify the email
we have a middleware in the kernel.php

in the routes,
add the middleware like this

```php
Route::get('/dashboard', function () {
    return view('dashboard');
})->middleware(['auth','verified'])->name('dashboard');
```
then in the user model we need to implement `MustVerifiedEmail`

```php
class User extends Authenticatable implements MustVerifyEmail

```

# Setup Login attempts 
in the `app\Http\Requests\Auth\LoginRequest.php` there is a method called `ensureIsNotRateLimited()`
this is where you can set it up

# Changing the logo of the auth views and dashboard

go to components/application-logo.blade.php and change the image or svg as simple as that.

# Logging in with username.


1. go to users migration and add a feild 
    `$table->string('username')->unique()`
2. also manually add a feild username in the database make it varchar make it nullable and unique.
3. add an input feild username in register view.
```php
    <!-- Username -->
        <div class="mt-4">
            <x-label for="username" :value="__('Username')" />

            <x-input id="username" class="block mt-1 w-full" type="text" name="username" :value="old('username')" required />
        </div>
```
4. Then in the user model add an entry to $fillable array
5. Same you can do for the login.
