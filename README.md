# Tips-Laravel-Mail-Config-Test

Ceci est une petite documentation de comment configurer et tester le mailing en Laravel

1:----------------------------Aller dans son compte Google et générer un mot de passe d'application

2:----------------------------CONFIGURER LE FICHIER ENV COMME SUIT:
MAIL_MAILER=smtp
MAIL_HOST=smtp.gmail.com
MAIL_PORT=587
MAIL_USERNAME=monEmail@gmail.com
MAIL_PASSWORD=mot_de_passe_email
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS=monEmail@gmail.com
MAIL_FROM_NAME="Le nom à affciher comme auteur sur le mail"
MAIL_PASSWORD=mot_de_passe_généré_par_compte_googel (SANS ESPACES)

3:--------------------------- VERIFIER config/mail.php:
return [
    'default' => env('MAIL_MAILER', 'smtp'),
    'mailers' => [
        'smtp' => [
            'transport' => 'smtp',
            'host' => env('MAIL_HOST', 'smtp.mailtrap.io'),
            'port' => env('MAIL_PORT', 2525),
            'encryption' => env('MAIL_ENCRYPTION', 'tls'),
            'username' => env('MAIL_USERNAME'),
            'password' => env('MAIL_PASSWORD'),
            'timeout' => null,
            'auth_mode' => null,
        ],
    ],
    'from' => [
        'address' => env('MAIL_FROM_ADDRESS', 'noreply@votreapp.com'),
        'name' => env('MAIL_FROM_NAME', 'Votre Application'),
    ],
];


4:---------------------------------------TESTER AVEC TINKER:
php artisan tinker
use Illuminate\Support\Facades\Mail;
Mail::raw('Ceci est un test d’envoi d’email.', function ($message) {
    $message->to('client@email.com')
        ->subject('Test d’email Laravel');
});



