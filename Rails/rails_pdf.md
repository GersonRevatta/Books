# PDF en Rails
> Hay muchas formas de generar archivos PDF en Ruby y Rails, pero nos centraremos en dos: Prawn y PDFKit. Prawn le da más control sobre la salida p mientras que PDFKit le permite usar lo que ya sabe (HTML) para generar archivos PDF desde la vista de Rails y el código de estilo.

##Opciones
1.[Prawn](https://github.com/prawnpdf/prawn)
2.[pdfkit](https://github.com/pdfkit/pdfkit)
3.[wicked](https://github.com/mileszs/wicked_pdf)




>Prawn es muy poderoso, y si necesita un control extremadamente preciso sobre la salida de PDF, es una buena opción. La desventaja, sin embargo, es que tiene que envolver su cabeza alrededor de su modelo de representación y aprender su DSL para diseñar documentos.

##En este caso usare wicked_pdf
Necesitare estas dos gemas:
```
  gem 'wicked_pdf'
  gem 'wkhtmltopdf-binary'
```

Una es la gema como tal , la otra es el resto de sus configuraciones

##Routes
```
  get :download_resume
```

>Creo un metodo en el controller en que quiera generar y descargar el pdf , o tambien podria crear un controller propio

```

    def download_resume
      @links = Link.all
      pdf = WickedPdf.new.pdf_from_string(
      render_to_string('links/index.html.haml', layout: false)
      )
      send_data pdf, :filename => 'resume.pdf', :type => 'application/pdf', :disposition => 'attachment'
    end
```

##Enlace de descarga
```

 =link-to 'download',  url-mehod

```

* Y eso seria todo
  [Tutorial de Referencia](https://imvishaltyagi444.wordpress.com/2016/03/04/pdf-file-create-and-download-by-wicked_pdf/)