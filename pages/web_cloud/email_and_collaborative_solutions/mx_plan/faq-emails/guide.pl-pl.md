---
title: FAQ e-mail OVHcloud
updated: 2020-05-05
---

## Najczęściej zadawane pytania dotyczące kont e-mail

### Co zrobić, jeśli nie mogę wysyłać/odbierać wiadomości e-mail?

W większości przypadków brak możliwości wysyłania/odbierania wiadomości e-mail wiąże się z konfiguracją adresu w programie pocztowym. Aby to sprawdzić, zaloguj się w interfejsie [webmail](https://www.ovh.pl/mail/){.external} i przeprowadź test wysyłania i odbierania wiadomości z Twojego adresu.

- Jeśli wszystko działa normalnie, to znaczy, że źródło problemu leży w konfiguracji oprogramowania.
- Jeśli natomiast wysyłanie lub odbieranie wciąż jest niemożliwe, masz do wyboru kilka rozwiązań.

Czy po wysłaniu e-maila na Twoje konto e-mail dostajesz komunikat błędu? Jeśli tak, zlokalizuj ten komunikat — znajdziesz w nim przyczynę problemów (przepełniona lub nieistniejąca skrzynka itp.).

Możesz także sprawdzić, czy Twoja domena dostarcza wiadomości e-mail we właściwe miejsce. W tym celu przejdź do [Panelu klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.pl/&ovhSubsidiary=pl){.external}, wybierz strefę DNS Twojej domeny i spójrz na ustawione wpisy typu MX. Wpisy te powinny mieć następujący format: „mx\*.mail.ovh.net.” (symbol „\*” zastąp cyfrą od 0 do 3).
Jeśli wpisy MX są różne, to znaczy, że być może korzystasz z oferty e-mail od innego operatora niż OVHcloud.

**Wskazówki i porady**: Jeśli nie możesz się zalogować do interfejsu webmail, to znaczy, że hasło może być błędne. Sprawdź hasło, a w razie potrzeby zmień je w [Panelu klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.pl/&ovhSubsidiary=pl){.external} i zaloguj się ponownie. W tym celu przejdź do [naszej dokumentacji](/pages/web_cloud/email_and_collaborative_solutions/troubleshooting/diagnostic_advanced).

### Jak skonfigurować mój adres e-mail i używać go w interfejsie webmail?

Konto e-mail można skonfigurować w programie pocztowym takim jak Outlook, Thunderbird, Mail na komputery Mac itd.
W tym celu przygotowaliśmy przewodniki, z których dowiesz się, jak skonfigurować Twój adres. Znajdziesz je na [tej stronie](/products/web-cloud-email-collaborative-solutions-mx-plan).

Za sprawą interfejsu [webmail](https://www.ovh.pl/mail/){.external} w każdej chwili możesz uzyskać dostęp do Twojej poczty za pośrednictwem dowolnego urządzenia z dostępem do Internetu. Po utworzeniu konta e-mail zaloguj się tam, aby uzyskać dostęp do poczty.

**Wskazówki i porady**: Jeśli konfigurujesz konto e-mail w programie pocztowym, zalecamy użycie protokołu IMAP. Dzięki temu wiadomości e-mail będą przechowywane na serwerze i będzie można uzyskać do nich dostęp z dowolnego miejsca za pomocą interfejsu [webmail](https://www.ovh.pl/mail/){.external}. W tym celu przejdź do [naszej dokumentacji](/pages/web_cloud/email_and_collaborative_solutions/mx_plan/email_generalities).

### Zarządzanie usługami e-mail

Wszystkimi Twoimi kontami e-mail zarządzasz w [Panelu klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.pl/&ovhSubsidiary=pl){.external}. Zaloguj się do Panelu klienta i przejdź do odpowiedniej usługi. Możesz zmienić hasła do kont e-mail, sprawdzić dostępne miejsce na każdym z kont, utworzyć nowe konta lub usunąć istniejące.

**Porady i podpowiedzi**: Dzięki rozwiązaniom poczty elektronicznej MX Plan możesz delegować uprawnienia do zarządzania kontem e-mail innemu kontu OVHcloud, jednocześnie zachowując nad nim kontrolę. Nadaj uprawnienia odpowiedniemu kontu w [Panelu klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.pl/&ovhSubsidiary=pl){.external}. W tym celu zaloguj się do Panelu klienta OVHcloud, przejdź do sekcji „Konta e-mail” i wybierz odpowiednią domenę. Następnie przejdź do zakładki „Konta e-mail” i wybierz opcję:

- `Zarządzaj elementami współdzielonymi przez wszystkie konta e-mail`{.action} po prawej stronie, jeśli chcesz delegować uprawnienia do zarządzania wszystkimi kontami dla tej domeny
- `Zarządzanie delegacjami uprawnień`{.action}, jeśli chcesz delegować uprawnienia do zarządzania określonym kontem (kliknij `...`{.action} obok konta)  

Pamiętaj, że w przypadku obu opcji wymagane jest podanie identyfikatora klienta OVHcloud (NIC).

### Jak ograniczyć ilość otrzymywanego spamu?

Aby ograniczyć liczbę wiadomości-śmieci, możesz skonfigurować filtry dla poczty e-mail (w ofercie MXPlan — „Filtrowanie”). Ich celem jest usunięcie lub przeniesienie tego typu wiadomości do folderu „Spam” w momencie ich odebrania.
W tym celu zaloguj się do [Panelu klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.pl/&ovhSubsidiary=pl){.external}, przejdź do rubryki `E-mail`, a następnie wybierz daną domenę, kartę `E-mail`{.action}, a potem w kolumnie `Filtrowanie`{.action} kliknij przycisk akcji.

Jeśli w Panelu klienta nie widzisz kolumny `Filtrowanie`{.action}, wówczas tworzenie filtrów odbywa się za pośrednictwem reguł zarządzania skrzynką odbiorczą w interfejsie [webmail](https://www.ovh.pl/mail/){.external}. Więcej szczegółów znajdziesz w przewodniku: [Reguły skrzynki odbiorczej w interfejsie OWA](/pages/web_cloud/email_and_collaborative_solutions/using_the_outlook_web_app_webmail/creating-inbox-rules-in-owa-mx-plan).

**Wskazówki i porady**: Jeśli włączysz filtr antyspamowy, możliwe, że niektóre prawidłowe wiadomości zostaną uznane za spam. Jest to tzw. wynik „fałszywie pozytywny”. Jeśli tak się zdarzy, zachęcamy do otwarcia zgłoszenia w [Panelu klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.pl/&ovhSubsidiary=pl){.external}, aby poinformować nas o tym. Dzięki temu będziemy mogli podjąć odpowiednie kroki, aby takie wiadomości nie były w przyszłości uznawane za spam.

### Mój adres e-mail jest zajęty. Nie mam już miejsca. Co mogę zrobić?

Jeśli zamówiłeś [jedną z naszych ofert e-mail OVHcloud](https://www.ovhcloud.com/pl/emails/) i jedno z Twoich kont e-mail jest zapełnione, zapoznaj się z naszym przewodnikiem "[Zarządzanie przestrzenią dyskową konta e-mail](/pages/web_cloud/email_and_collaborative_solutions/troubleshooting/email_manage_quota)". Przewodnik ten pomoże Ci określić, czy możesz zoptymalizować istniejącą przestrzeń lub czy konieczna jest zmiana oferty e-mail w celu zwiększenia przestrzeni dyskowej.

### Chcę zmienić ofertę e-mail na mój adres. Jak mogę to zrobić zachowując jej zawartość?

Chcesz zmienić [ofertę e-mail](https://www.ovhcloud.com/pl/emails/) na większą przestrzeń i więcej funkcji, ale chcesz zachować zawartość swojego istniejącego adresu. W tym celu skorzystaj z jednego z naszych przewodników:

- [Przeniesienie adresu e-mail MX Plan na konto E-mail Pro lub Exchange](/pages/web_cloud/email_and_collaborative_solutions/migrating/migration_control_panel)
- [Przenoszenie adresów e-mail z jednej platformy e-mail OVHcloud na inną](/pages/web_cloud/email_and_collaborative_solutions/migrating/migration_control_panel)
- [Ręczna migracja Twojego konta e-mail](/pages/web_cloud/email_and_collaborative_solutions/migrating/manual_email_migration)
- [Przeniesienie kont e-mail za pomocą OVH Mail Migrator](/pages/web_cloud/email_and_collaborative_solutions/migrating/migration_omm)
- [Przeniesienie konta Gmail do konta e-mail OVHcloud za pośrednictwem OVH Mail Migrator](/pages/web_cloud/email_and_collaborative_solutions/migrating/security_gmail)

### Czy oferta Office 365 Pro Plus zawiera licencję Skype?

Oferta Office 365 Pro Plus nie zawiera licencji Skype. W ofercie zawarty jest jedynie program Skype for Business.

## Sprawdź również

Dołącz do społeczności naszych użytkowników na stronie <https://community.ovh.com/en/>.
