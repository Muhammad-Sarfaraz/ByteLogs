# Life cycle
index.php -> bootstrap/app.php -> App\Http\Kernel -> Middleware -> Router -> Controller -> Service Providers -> Eloquent ORM (Optional) -> Response -> Middleware (Outgoing) -> Termination -> Browser Response
