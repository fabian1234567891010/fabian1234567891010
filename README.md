- 👋 Hi, I’m @fabian1234567891010
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
fabian1234567891010/fabian1234567891010 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->from django.db import models

class Wiadomosc(models.Model):
    numer_telefonu = models.CharField(max_length=15)
    tresc = models.TextField()
    data = models.DateTimeField(auto_now_add=True)

# Przykładowy widok Django do pobierania wiadomości po zalogowaniu
from django.shortcuts import render
from django.http import HttpResponse
from django.contrib.auth.decorators import login_required

@login_required
def wiadomosci_dla_numeru(request):
    # Pobierz numer telefonu z zalogowanego użytkownika
    numer_uzytkownika = request.user.profile.numer_telefonu  # Załóżmy, że numer telefonu jest przechowywany w polu numer_telefonu profilu użytkownika

    # Pobierz wszystkie wiadomości dla danego numeru telefonu
    wiadomosci = Wiadomosc.objects.filter(numer_telefonu=numer_uzytkownika)

    # Wyświetl wiadomości na stronie
    return render(request, 'wiadomosci.html', {'wiadomosci': wiadomosci})
