Symfony2-override-error-pages
================================

Symfony2 Override/Customize Error Pages

In Symfony 2 if you want to override/customize error pages like 404/500 etc,you can easily override error service which is `twig.controller.exception` create your service with same name and change the controller class for it as below

        parameters:
            twig.controller.exception.class: Acme\DemoBundle\Controller\ExceptionController
        services:
            twig.controller.exception:
                class: %twig.controller.exception.class%
                arguments: [ '@twig' ,'%kernel.debug%' ,'@service_container']


In above service i have additionaly passed `@service_container` service to get the some data to display on error pages, like in repo code i have accessed my service which contains header/footer menus, do what ever you need since you have a container

Now to override view for error pages add your new file at `app\Resources\TwigBundle\views\Exception\error.html.twig`

Note it will work in production mode only

And the last part import your serivce file in main configuration file

        imports:
            - { resource: parameters.yml }
            - { resource: security.yml }
            - { resource: @AcmeDemoBundle/Resources/config/twig_service.yml }
