# 8

Here’s how you can create a simple registration page in Laravel:

---

### Step 1: Create a Laravel Application
1. Open your terminal and create a new Laravel application:
   ```bash
   composer create-project laravel/laravel RegistrationApp
   cd RegistrationApp
   ```

2. Run the Laravel development server:
   ```bash
   php artisan serve
   ```

---

### Step 2: Create the Registration View
1. Inside the `resources/views` directory, create a file named `register.blade.php`:
   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Registration Page</title>
   </head>
   <body>
       <h1>Register</h1>
       <form action="{{ route('submit.registration') }}" method="POST">
           @csrf
           <label for="name">Name:</label>
           <input type="text" name="name" id="name" required><br><br>
           <label for="id">ID:</label>
           <input type="text" name="id" id="id" required><br><br>
           <label for="cgpa">CGPA:</label>
           <input type="text" name="cgpa" id="cgpa" required><br><br>
           <button type="submit">Register</button>
       </form>
   </body>
   </html>
   ```

---

### Step 3: Create Routes
1. Open the `routes/web.php` file and add the following routes:
   ```php
   use App\Http\Controllers\RegistrationController;

   Route::get('/register', [RegistrationController::class, 'showForm'])->name('show.registration');
   Route::post('/register', [RegistrationController::class, 'submitForm'])->name('submit.registration');
   ```

---

### Step 4: Create the Controller
1. Run the following command to create a controller:
   ```bash
   php artisan make:controller RegistrationController
   ```

2. Open `app/Http/Controllers/RegistrationController.php` and add the following code:
   ```php
   namespace App\Http\Controllers;

   use Illuminate\Http\Request;

   class RegistrationController extends Controller
   {
       // Show the registration form
       public function showForm()
       {
           return view('register');
       }

       // Handle form submission
       public function submitForm(Request $request)
       {
           $name = $request->input('name');
           $id = $request->input('id');
           $cgpa = $request->input('cgpa');

           return view('details', compact('name', 'id', 'cgpa'));
       }
   }
   ```

---

### Step 5: Create the Details View
1. Inside the `resources/views` directory, create a file named `details.blade.php`:
   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Submitted Details</title>
   </head>
   <body>
       <h1>Submitted Details</h1>
       <p><strong>Name:</strong> {{ $name }}</p>
       <p><strong>ID:</strong> {{ $id }}</p>
       <p><strong>CGPA:</strong> {{ $cgpa }}</p>
   </body>
   </html>
   ```

---

### Testing the Application
1. Start the server:
   ```bash
   php artisan serve
   ```

2. Visit `http://127.0.0.1:8000/register` in your browser.
3. Fill out the form and click **Register**.
4. The submitted details will be displayed on a new page.

---

This implementation is simple, beginner-friendly, and easy to understand.







Here’s a simple step-by-step implementation of a **Login System** in Laravel with clear and easy-to-follow instructions:

---

### Step 1: Create a Laravel Application
1. Create a new Laravel application (if you haven't already):
   ```bash
   composer create-project laravel/laravel LoginApp
   cd LoginApp
   ```

2. Start the Laravel development server:
   ```bash
   php artisan serve
   ```

---

### Step 2: Create the Login View
1. Inside the `resources/views` directory, create a file named `login.blade.php`:
   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Login Page</title>
   </head>
   <body>
       <h1>Login</h1>
       <form action="{{ route('submit.login') }}" method="POST">
           @csrf
           <label for="username">Username:</label>
           <input type="text" name="username" id="username" required><br><br>
           <label for="password">Password:</label>
           <input type="password" name="password" id="password" required><br><br>
           <button type="submit">Login</button>
       </form>
   </body>
   </html>
   ```

---

### Step 3: Create Routes
1. Open the `routes/web.php` file and add these routes:
   ```php
   use App\Http\Controllers\LoginController;

   Route::get('/login', [LoginController::class, 'showLogin'])->name('show.login');
   Route::post('/login', [LoginController::class, 'submitLogin'])->name('submit.login');
   Route::get('/profile', [LoginController::class, 'showProfile'])->name('show.profile');
   ```

---

### Step 4: Create the Controller
1. Generate a new controller:
   ```bash
   php artisan make:controller LoginController
   ```

2. Open `app/Http/Controllers/LoginController.php` and add the following code:
   ```php
   namespace App\Http\Controllers;

   use Illuminate\Http\Request;

   class LoginController extends Controller
   {
       // Show the login form
       public function showLogin()
       {
           return view('login');
       }

       // Handle login submission
       public function submitLogin(Request $request)
       {
           $username = $request->input('username');
           $password = $request->input('password');

           // Dummy validation (replace with database validation in real apps)
           if ($username === 'admin' && $password === 'password') {
               return redirect()->route('show.profile')->with('success', 'Login successful!');
           }

           return redirect()->route('show.login')->with('error', 'Invalid username or password.');
       }

       // Show profile view
       public function showProfile()
       {
           return view('profile');
       }
   }
   ```

---

### Step 5: Create the Profile View
1. Inside the `resources/views` directory, create a file named `profile.blade.php`:
   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Profile</title>
   </head>
   <body>
       <h1>Welcome to Your Profile!</h1>
       <p>You have successfully logged in.</p>
       <a href="{{ route('show.login') }}">Logout</a>
   </body>
   </html>
   ```

---

### Step 6: Add Flash Messages (Optional but Helpful)
1. To display success or error messages, add the following to the `login.blade.php`:
   ```html
   @if (session('success'))
       <p style="color: green;">{{ session('success') }}</p>
   @endif

   @if (session('error'))
       <p style="color: red;">{{ session('error') }}</p>
   @endif
   ```

---

### Testing the Application
1. Start the server:
   ```bash
   php artisan serve
   ```

2. Visit `http://127.0.0.1:8000/login` in your browser.
3. Enter the username `admin` and password `password` to log in successfully.
4. If the login is correct, you'll be redirected to the **Profile** page. Otherwise, you'll see an error message.

---

### Summary
This implementation is:
- **Easy to Understand**: Clear flow of routes, views, and controllers.
- **Simple to Write**: Minimal code to handle login logic.
- **Flexible**: Ready to integrate database validation for real-world applications. 

Let me know if you'd like further enhancements! 🚀





