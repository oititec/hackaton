
# Hackathon - Desafios e Ferramentas de Ajuda (Opcionais)

## Desafio 1: Captura de Documentos + OCR + Validação Antifraude

### Descrição do Desafio
Neste desafio, as equipes devem criar um sistema que:
1. Capture a imagem de um documento (ex: RG, CNH, Passaporte);
2. Classifique automaticamente o tipo do documento;
3. Extraia os dados usando OCR (Reconhecimento Óptico de Caracteres) com alta acurácia;
4. Valide o documento, detectando possíveis fraudes visuais ou digitais.

### Ferramenta de ajuda (Opcional): Serviço de OCR

Disponibilizamos um serviço (teste) de OCR que auxilia na extração parcial das informações. Você pode utilizar o seguinte exemplo de chamada API para integrar o OCR em seu sistema:

```bash
curl --location 'https://ocr-api-wn5au7wnba-rj.a.run.app/api/v1/documents/process-file' \
--header 'Content-Type: application/json' \
--form 'images.mode="split"' \
--form 'images.data.split.front=@"/home/oiti/front.jpg"' \
--form 'images.data.split.back=@"/home/oiti/back.png"'
```


## Possíveis Saídas do OCR

A seguir, são apresentadas as possíveis saídas para os tipos de documentos esperados:

1. CNH (Carteira Nacional de Habilitação)
```json
{
  "documentType": "CNH",
  "name": "Nome Completo do Condutor",
  "cnhNumber": "Número do Registro da CNH composto por 11 caracteres",
  "rgNumber": "Número do Documento de Identidade utilizado para CNH",
  "rgIssuingAuthority": "Órgão Expedidor (ex: SSP/SP)",
  "cpfNumber": "Número do CPF",
  "birthDate": "Data de Nascimento (formato YYYY-MM-DD)",
  "fatherName": "Nome do Pai (se visível)",
  "motherName": "Nome da Mãe (se visível)",
  "placeOfBirth": "Cidade/Estado de Naturalidade (se visível)",
  "issuingAuthority": "Órgão Emissor (ex: SSP/MG, DETRAN/MG)",
  "issueDate": "Data de Emissão da CNH (formato YYYY-MM-DD)",
  "validUntil": "Data de Validade da CNH (formato YYYY-MM-DD)",
  "firstLicenseDate": "Data da Primeira Habilitação (formato YYYY-MM-DD)",
  "category": "Categoria da Habilitação com no máximo duas siglas",
  "stateOfDocIdentity": "UF do Documento de Identidade",
  "placeOfIssue": "Local de Emissão (Cidade/UF)",
  "renach": "Número do RENACH (Fica no verso do documento)",
  "gender": "M OU F",
  "nationality": "Nacionalidade"
}
```

2. CIN (Carteira de Identidade Nacional)
```json
{
  "documentType": "CIN",
  "name": "Nome Completo da Pessoa",
  "rgNumber": "Número do RG",
  "state": "Sigla do Estado (ex: MG)",
  "issuingAuthority": "Órgão Expedidor (ex: SSP/SP)",
  "issueDate": "Data de Emissão (formato YYYY-MM-DD)",
  "cpfNumber": "Número do CPF (se visível)",
  "birthDate": "Data de Nascimento (formato YYYY-MM-DD)",
  "fatherName": "Nome do Pai (se visível)",
  "motherName": "Nome da Mãe (se visível)",
  "placeOfBirth": "Cidade/Estado de Naturalidade (se visível)",
  "civilRegistry": "Informações do Registro Civil",
  "electorTitle": "Número do Título de Eleitor",
  "ctpsNumber": "Número da Carteira de Trabalho",
  "ctpsSeries": "Série da CTPS",
  "ctpsUF": "UF de Emissão da CTPS",
  "nisPispasep": "Número NIS/PIS/PASEP",
  "professionalID": "Identidade Profissional",
  "militaryCertificate": "Número do Certificado Militar",
  "gender": "M OU F",
  "nationality": "Brasileira",
  "directorSignature": "Assinatura do Diretor do Órgão Expedidor",
  "fingerprint": "Indicação da Impressão Digital",
  "documentVersion": "Indicação da Via do Documento"
}
```

3. RG (Registro Geral)
```json
{
  "documentType": "RG",
  "name": "Nome Completo da Pessoa",
  "rgNumber": "Número do RG",
  "state": "Sigla do Estado (ex: MG)",
  "issuingAuthority": "Órgão Expedidor (ex: SSP/SP)",
  "issueDate": "Data de Emissão (formato YYYY-MM-DD)",
  "cpfNumber": "Número do CPF (se visível)",
  "birthDate": "Data de Nascimento (formato YYYY-MM-DD)",
  "fatherName": "Nome do Pai (se visível)",
  "motherName": "Nome da Mãe (se visível)",
  "placeOfBirth": "Cidade/Estado de Naturalidade (se visível)",
  "civilRegistry": "Informações do Registro Civil",
  "electorTitle": "Número do Título de Eleitor",
  "ctpsNumber": "Número da Carteira de Trabalho",
  "ctpsSeries": "Série da CTPS",
  "ctpsUF": "UF de Emissão da CTPS",
  "nisPispasep": "Número NIS/PIS/PASEP",
  "professionalID": "Identidade Profissional",
  "militaryCertificate": "Número do Certificado Militar",
  "gender": "M OU F",
  "nationality": "Brasileira",
  "directorSignature": "Assinatura do Diretor do Órgão Expedidor",
  "fingerprint": "Indicação da Impressão Digital",
  "documentVersion": "Indicação da Via do Documento"
}
```

Caso o sistema não consiga processar um documento corretamente, a resposta será:
```json
{
  "documentType": null,
  "rejectionReason": "Breve explicação do motivo"
}
```


## Desafio 2: Liveness Detection

### Descrição do Desafio
O objetivo do Desafio 2 é criar um mecanismo de liveness detection (detecção de vida) que funcione em tempo real e garanta que:
1. A pessoa está fisicamente presente;
2. Não é uma foto, vídeo ou máscara;
3. A captura é feita no momento da transação.

### Ferramentas de ajuda (Opcionais)

Disponibilizamos duas ferramentas comerciais parceiras que podem ser utilizadas para a detecção de liveness (passivo). Essas ferramentas podem ser integradas no seu projeto, caso a equipe tenha interesse:

Recognito:

Link: [Recognito Face Liveness Detection](https://github.com/recognito-vision/Linux-FaceRecognition-FaceLivenessDetection/tree/main/LivenessDetection-Demo)

Kby:

Link: [Kby Face Liveness Detection](https://github.com/kby-ai/FaceLivenessDetection-Docker)


## Licenciamento

As licenças para o OCR e para as ferramentas de liveness detection devem ser solicitadas ao Pedro/Administração. Por favor, entre em contato para mais informações sobre a obtenção das licenças necessárias.
