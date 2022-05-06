+++
date        = "2022-05-06"
title       = "Pujada d'arxius"
description = "Pujada d'arxius al servidor."
sections    = "Canigó. Documentació Versió 3.6"
weight      = 5
+++

## Propòsit

Aquest mòdul permet al servidor obtenir fitxers adjunts als formularis HTML de client. A més aquest mòdul permet llegir el fitxer de forma directa, deser-lo al sistema de fitxers, emmagatzemar-lo en una base de dades o enllaçar-ho amb altres mòduls com pot ser el servei d'antivirus.

## Instal.lació i Configuració

### Instal.lació

Per tal d'instal-lar el mòdul d'upload de fitxers es pot incloure automàticament a través de l'eina de suport al desenvolupament o bé afegir manualment en el pom.xml de l'aplicació la següent dependència:

```xml
<dependency>
  <groupId>cat.gencat.ctti</groupId>
  <artifactId>canigo.support.fileupload</artifactId>
  <version>${canigo.support.fileupload.version}</version>
</dependency>
```

A la [Matriu de Compatibilitats 3.6] (/canigo-download-related/matrius-compatibilitats/canigo-36/) es pot comprovar la versió del mòdul compatible amb la versió de Canigó utilitzada.

### Configuració

La configuració es realitza automàticament a partir de la eina de suport al desenvolupament.

Ubicació proposada: <PROJECT_ROOT>/src/main/resources/config/props/fileupload.properties

Propietat | Requerit | Descripció
--------- | -------- | ----------
*.fileUpload.defaultEncoding | No | Direcció IP del servidor Engine Scan del CTTI, responsable dels escaneigs.
*.fileUpload.maxUploadSize   | No | Màxim tamany permés abans que es rebutgin els fitxers. Valor per defecte: -1(no hi ha límit).
*.fileUpload.maxInMemorySize | No | Màxim tamany permés en bytes abans de guardar en disc. Valor per defecte: 10240 (bytes).
*.fileUpload.launchExceptionIfVirusDetected | No | Opció només disponible per a la integració del fileupload i antivirus. Indica si es llençarà una excepció al servei en el cas de que es trobi un virus en l'arxiu pujat. Valor per defecte: true.

## Utilització del Mòdul

### Exemple d'ús

**FileUploadController.java**

Endpoint de l'aplicació que fa servir el mètode getUploadedFiles() escanejant amb el servei d'antivirus els fitxers que es volen pujar.

El mòdul de Pujada d'arxius ja té la dependència transitiva del mòdul d'antivirus per tant no caldrà afegir el mòdul ni modificar el pom.xml
Però en cas de fer servir (com és el cas a aquest exemple d'ús) l'escaneig de fixers amb l'antivirus, caldrà configurar aquest mòdul, podeu consultar <a href="/canigo-documentacio-versions-36/integracio/modul-antivirus/">Mòdul Antivirus</a>

```java
    package cat.gencat.canigo36fileupload.endpoints;

    import cat.gencat.ctti.canigo.arch.integration.antivirus.ResultatEscaneig;
    import cat.gencat.ctti.canigo.arch.integration.antivirus.exceptions.AntivirusException;
    import cat.gencat.ctti.canigo.arch.support.fileupload.UploadedFiles;
    import cat.gencat.ctti.canigo.arch.support.fileupload.impl.FileUploadServiceAntivImpl;
    import org.apache.logging.log4j.LogManager;
    import org.apache.logging.log4j.Logger;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.http.MediaType;
    import org.springframework.web.bind.annotation.PostMapping;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RequestParam;
    import org.springframework.web.bind.annotation.RestController;
    import org.springframework.web.multipart.MultipartFile;
    import org.springframework.web.multipart.MultipartHttpServletRequest;

    import java.io.IOException;

    @RestController
    @RequestMapping("/fileupload")
    public class FileUploadController {
      private static Logger log = LogManager.getLogger(FileUploadController.class.getName());

      @Autowired
      private FileUploadServiceAntivImpl fileUploadService;

      @PostMapping(produces = { MediaType.APPLICATION_JSON_VALUE })
      public ResultatEscaneig fileUpload(MultipartHttpServletRequest request, @RequestParam MultipartFile file) throws IOException, AntivirusException {
        log.info("file: ", file.getName());
        UploadedFiles uploadedFiles = fileUploadService.getUploadedFiles(request, file.getName());
        log.info("uploadedFiles.hasFiles: ", uploadedFiles.hasFiles());

        return fileUploadService.getAntivirus().scan(file.getBytes());
      }
    }
```