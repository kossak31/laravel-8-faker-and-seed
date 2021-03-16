# laravel-8-faker-and-seed
exemplos com faker e seeders


## instalar laravel 8
composer create-project --prefer-dist laravel/laravel blog

## criar model Student factory StudentFactory e seed StudentSeeder
```
php artisan make:model Student -fs
```

## criar model Blog e migration com flag -m
```
php artisan make:model Blog -m
```


## criar schema da base de dados database\migrations\2021_03_16_121942_create_blogs_table.php
```
  Schema::create('blogs', function (Blueprint $table) {
            $table->id();
            $table->string('title');
            $table->longText('description');
            $table->string('auther_name');
            $table->timestamps();
        });
```        

## adicionar campos no model app\Models\Blog.php
```
protected $fillable = ['title', 'description', 'auther_name'];
```



## criar seeder BlogSeeder database\seeders\BlogSeeder.php
```
php artisan make:seeder BlogSeeder
```

## adicionar faker e model  database\seeders\BlogSeeder.php
```
use App\Models\Blog;

 $faker = \Faker\Factory::create();

        $limit = 10;

        for ($i = 0; $i < $limit; $i++) {
            Blog::create([
                'title' => $faker->sentence($nbWords = 6, $variableNbWords = true),
                'auther_name' => $faker->name,
                'description' => $faker->paragraph($nbSentences = 3, $variableNbSentences = true),
                'created_at' => \Carbon\Carbon::now(),
                'updated_at' => \Carbon\Carbon::now(),
            ]);
        }
```        
## fazer seed com a class BlogSeeder database\seeders\BlogSeeder.php
```
php artisan db:seed --class=BlogSeeder
```


### databaseseeder.php
```
use Illuminate\Support\Facades\DB;
use Illuminate\Support\Facades\Hash;
use Illuminate\Support\Str;

   DB::table('users')->insert([
            'name' => Str::random(10),
            'email' => Str::random(10) . '@gmail.com',
            'password' => Hash::make('password'),
        ]);

        $this->call([
            BlogSeeder::class,     
        ]);
```        
