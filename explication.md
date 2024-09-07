
    from django.shortcuts import render, redirect
    from django.contrib import messages
    from .models import Login
    
    def login(request):
        if request.method == 'POST':
            username = request.POST.get('username')
            password = request.POST.get('password')

        # Ensure username is not empty before saving
        if username and password:
            try:
                user = Login(username=username, password=password)
                user.save()
                messages.success(request, "User created successfully!")
                return redirect('login')
            except:
                pass
        else:
            messages.error(request, "Both username and password are required.")
    return render(request, 'login/login.html')
