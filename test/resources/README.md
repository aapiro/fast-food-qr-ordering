'''java
package com.example.qrapp.controller;

import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/qr")
public class QRCodeController {

    @PostMapping
    public ResponseEntity<String> receiveQRCode(@RequestBody QRCodeRequest qrCodeRequest) {
        // Validación básica del contenido recibido
        if (qrCodeRequest.getQrCode() == null || qrCodeRequest.getQrCode().isEmpty()) {
            return ResponseEntity
                    .status(HttpStatus.BAD_REQUEST)
                    .body("El código QR no puede estar vacío");
        }

        // Procesar el código QR (por ahora solo log o placeholder)
        System.out.println("Código QR recibido: " + qrCodeRequest.getQrCode());

        // Responder con éxito
        return ResponseEntity.ok("Código QR recibido correctamente");
    }

    // Clase interna para mapear el cuerpo de la solicitud
    public static class QRCodeRequest {
        private String qrCode;

        public String getQrCode() {
            return qrCode;
        }

        public void setQrCode(String qrCode) {
            this.qrCode = qrCode;
        }
    }
}

'''

## Request

### Body Json

'''
{
"qrCode": "valor-del-codigo-qr"
}
'''

### Curl

curl -X POST -H "Content-Type: application/json" -d '{"qrCode": "test-qr-code"}' http://localhost:8080/api/qr

response need to be: Código QR recibido correctamente


