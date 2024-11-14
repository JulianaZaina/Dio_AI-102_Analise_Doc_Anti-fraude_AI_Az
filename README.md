# Dio_AI-102_Analise_Doc_Anti-fraude_AI_Az
Desafio de Projeto 2 DIO Análise de Documento Anti-fraude AI-102

Criar um recurso da IA do Azure para Informação de Documentos e obter os dados da conexão, seguir as etapas:
- No portal do Azure, selecione Criar um recurso.
- Na caixa Pesquisar serviços e marketplace, digite Informação de Documentos e pressione Enter.
- Na página Informação de Documentos, selecione Criar.
- Na página Criar Informação de Documentos, em Detalhes do Projeto, selecione sua Assinatura e crie um novo Grupo de recursos
- Em Detalhes da instância, selecione a Região 
- Na caixa de texto Nome, digite um nome exclusivo para o recurso.
- Selecione um Tipo de preço e selecione Examinar + criar. 
- Se os testes de validação forem aprovados, selecione Criar. O Azure implanta o novo recurso de IA do Azure para Informação de Documentos.

EXECUÇÃO:
 
Ao criar um aplicativo que usa a IA do Azure para Informação de Documentos copiar duas informações para se conectar ao recurso:
Ponto de extremidade. Essa é a URL em que o recurso pode ser contatado. Endpoint
Chave de acesso. Essa é uma cadeia de caracteres exclusiva que o Azure usa para autenticar a chamada à IA do Azure para Informação de Documentos. Key 1 e Key 2 
KEY 1 A62jN9a3wPYKtJ1tnxw8NAQS0yg3T5zCYKoyBvL4aKAArGxmGEBbJQQJ99AKACYeBjFXJ3w3AAALACOG3BZM
KEY 2 BxF5wlRMeNNK7XVc33H4iz4FYZMWFnIMHQpuGxF6HegN92XoTXKYJQQJ99AKACYeBjFXJ3w3AAALACOGJNm5
ENDPOINT: https://desafioai102-bootcamp-doc-antifraude-002.cognitiveservices.azure.com/

Grupo de recurso: desafioai102-bootcamp-doc-antifraude-002
- Escolher modelo pre built
- Análise de dados

# CÓDIGO
This code sample shows Prebuilt Business Card operations with the Azure Form Recognizer client library. 
The async versions of the samples require Python 3.6 or later.
from azure.core.credentials import AzureKeyCredential
from azure.ai.formrecognizer import DocumentAnalysisClient

endpoint = "https://desafioai102-bootcamp-doc-antifraude-002.cognitiveservices.azure.com/"
key = "A62jN9a3wPYKtJ1tnxw8NAQS0yg3T5zCYKoyBvL4aKAArGxmGEBbJQQJ99AKACYeBjFXJ3w3AAALACOG3BZM "
# sample document
formUrl = "https://raw.githubusercontent.com/Azure-Samples/cognitive-services-REST-api-samples/master/curl/form-recognizer/business-card-english.jpg"
document_analysis_client = DocumentAnalysisClient(
    endpoint=endpoint, credential=AzureKeyCredential(key)
)
poller = document_analysis_client.begin_analyze_document_from_url("prebuilt-businessCard", formUrl)
business_cards = poller.result()
for idx, business_card in enumerate(business_cards.documents):
    print("--------Analyzing business card #{}--------".format(idx + 1))
    contact_names = business_card.fields.get("ContactNames")
    if contact_names:
        for contact_name in contact_names.value:
            print(
                "Contact First Name: {} has confidence: {}".format(
                    contact_name.value["FirstName"].value,
                    contact_name.value[
                        "FirstName"
                    ].confidence,))
            print(
                "Contact Last Name: {} has confidence: {}".format(
                    contact_name.value["LastName"].value,
                    contact_name.value[
                        "LastName"
                    ].confidence,)  )
    company_names = business_card.fields.get("CompanyNames")
    if company_names:
        for company_name in company_names.value:
            print(
                "Company Name: {} has confidence: {}".format(
                    company_name.value, company_name.confidence))
    departments = business_card.fields.get("Departments")
    if departments:
        for department in departments.value:
            print(
                "Department: {} has confidence: {}".format(
                    department.value, department.confidence)  )
    job_titles = business_card.fields.get("JobTitles")
    if job_titles:
        for job_title in job_titles.value:
            print(
                "Job Title: {} has confidence: {}".format(
                    job_title.value, job_title.confidence  ))
    emails = business_card.fields.get("Emails")
    if emails:
        for email in emails.value:
            print(
                "Email: {} has confidence: {}".format(email.value, email.confidence))
    websites = business_card.fields.get("Websites")
    if websites:
        for website in websites.value:
            print(
                "Website: {} has confidence: {}".format(
                    website.value, website.confidence))
    addresses = business_card.fields.get("Addresses")
    if addresses:
        for address in addresses.value:
            print(
                "Address: {} has confidence: {}".format(
                    address.value, address.confidence))
    mobile_phones = business_card.fields.get("MobilePhones")
    if mobile_phones:
        for phone in mobile_phones.value:
            print(
                "Mobile phone number: {} has confidence: {}".format(
                    phone.content, phone.confidence  )  )
    faxes = business_card.fields.get("Faxes")
    if faxes:
        for fax in faxes.value:
            print(
                "Fax number: {} has confidence: {}".format(
                    fax.content, fax.confidence) )
    work_phones = business_card.fields.get("WorkPhones")
    if work_phones:
        for work_phone in work_phones.value:
            print(
                "Work phone number: {} has confidence: {}".format(
                    work_phone.content, work_phone.confidence   ) )
    other_phones = business_card.fields.get("OtherPhones")
    if other_phones:
        for other_phone in other_phones.value:
            print(
                "Other phone number: {} has confidence: {}".format(
                    other_phone.value, other_phone.confidence      )     )
    print("----------------------------------------")
