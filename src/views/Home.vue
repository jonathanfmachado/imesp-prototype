<template>
  <div class="home">
    <!-- <b-alert show>Default Alert</b-alert> -->

    <b-container>
      <b-row>
        <b-col>
          Caderno:
          <b-form-select :options="cadernos" value="1"></b-form-select>
        </b-col>
        <b-col>
          Tipo:
          <b-form-select :options="tipoMateria" value="2"></b-form-select>
        </b-col>
        <b-col>
          Data Publicação:
          <b-form-input type="date" value="2019-07-16"></b-form-input>
        </b-col>
        <b-col>
          Seção:
          <b-form-select :options="secao" value="1"></b-form-select>
        </b-col>
      </b-row>
    </b-container>
    <hr style="margin: 25px 0">
    <b-container>
      <b-row style="justify-content: flex-end; ">
        <b-alert
          style="padding: 0.3rem 1.25rem !important; margin-bottom: 0.2rem;"
          variant="success"
          show
        >
          Valor
          <strong>
            <!-- {{getPrice(storyText)}} -->
            {{getPriceCmPorCol(storyText)}}
          </strong>
        </b-alert>
      </b-row>
      <b-row>
        <b-col>
          <span style="font-size:13px; aligment:left">
            Insira a matéria abaixo ou
            <a
              @click="openFileDialog()"
              style="color:#008eff; text-decoration:underline"
            >clique aqui para fazer o upload do arquivo.</a>
          </span>
          <form>
            <textarea name="editor1" id="editor1" rows="10" cols="80" v-model="storyText"></textarea>
          </form>
        </b-col>
        <b-col style="background:#c6c6c6; padding: 1rem;">
          <span style="display:block; margin-bottom: 1rem;" @click="refresh()">Preview</span>
          <!-- HTML title specified via default slot -->
          <div v-if="showWarning">
            <b-tooltip
              v-for="word in palavras"
              v-bind:key="word.id"
              :target="word.id.toString()"
              placement="bottom"
            >
              <div style>
                A publicação da palavra
                <strong>{{word.text}}</strong> é restrita.
              </div>
            </b-tooltip>
          </div>
          <div
            style="background:white; max-width: 300px;, height:100%; font-size: x-small; text-align: justify; padding: 10px;"
            v-html="storyText"
          ></div>
        </b-col>
      </b-row>
    </b-container>
    <input id="file-input" type="file" name="name" style="display: none;">
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "home",
  components: {
    HelloWorld
  },
  mounted() {
    CKEDITOR.config.height = 350;
    CKEDITOR.replace("editor1");
    // On changes:
    //     CKEDITOR.instances.editor1.on( 'change', () => {
    //     this.refresh()
    // } );
  },
  data() {
    return {
      palavras: [
        { text: "Considerando", id: 1 },
        { text: "fundamento", id: 2 },
        { text: "CONVOLAR", id: 3 }
      ],
      showWarning: false,
      precoMateria: 0,
      cadernos: [
        { value: null, text: "Selecione o Caderno" },
        { value: 1, text: "Empresarial" },
        { value: 2, text: "Executivo I" },
        { value: 2, text: "Executivo II" }
      ],
      secao: [
        { value: null, text: "Selecione a Seção" },
        { value: 1, text: "IOSP-Teste" }
      ],
      tipoMateria: [
        { value: null, text: "Selecione o Tipo da Matéria" },
        { value: 1, text: "Não especificado" },
        { value: 2, text: "Outro" }
      ],
      storyText:
        "<p><strong>Deliberação do Superintendente, de 21-5-19</strong></p>\
<p>Protocolo Ipem-SP 201906008 – 2019 – Processo 421 Interessado: J. W. N. Transportes Ltda. Considerando o que consta nos autos, em especial a manifestação do Centro de Verificação Veicular (MLFVE) (fl. 05), ratificada pelo Diretor do Departamento de Metrologia Legal e Fiscalização (DMLF) (fl. 05-vº), aliado à manifestação do Diretor de Divisão do Centro de Gestão de Processos (AGGEP) (fls. 06/07-vº), nos quais sugerem a apreensão definitiva do Certificado de Verificação de Veículo-Tanque Rodoviário (fl. 03) em razão da lavratura do Auto de Apreensão 385.292 em face da empresa J. W. N. Transportes Ltda, CNPJ 58.014.564/0001- 63 (fl. 02), cujas razões acolho como fundamento e DETERMINO, no desempenho de minhas atribuições legais elencadas no Decreto 55.964/2010, alterado pelo Decreto 64.110/2019 e com fulcro no parágrafo 2º, do artigo 5º do Regulamento Administrativo aprovado pela Resolução Conmetro 8/2006: I. CONVOLAR EM DEFINITIVA a apreensão cautelar do Certificado de Verificação de Veículo-Tanque Rodoviário 1134311, de 7-4-17, pertencente ao veículo-tanque, marca Gotti, placa CNR-0845, em virtude da não conformidade descrita no Auto de Apreensão 385.292 de 13-2-19 II. INVALIDAR o referido certificado, preservando suas informações e integridade, mantendo-o no corpo deste capeado para eventual consulta III. NOTIFICAR o interessado do teor da presente decisão, via publicação em Diário Oficial do Estado de São Paulo, concedendo- -lhe o prazo de 10 dias para requerer o que entender de direito, nos termos do artigo 20 do Regulamento Administrativo Aprovado pela Resolução Conmetro 8/06; assim, nesse prazo, os autos ficarão disponíveis para vistas, podendo ser requerida no Setor de Atendimento Jurídico, na Sede do Ipem-SP, situada na Rua Santa Cruz, 1.922, térreo, Vila Gumercindo, São Paulo – SP, no horário das 9h às 16h IV. FIXAR o prazo de 20 (VINTE) DIAS, a contar do término do interregno estabelecido no item antecedente, no caso de não manifestação do interessado, para efetivação das providências enunciadas no item II.</p>\
<p><strong>Deliberação do Superintendente, de 21-5-19</strong></p>\
<p>Protocolo Ipem-SP 201906009 – 2019 – Processo 422 Interessado: J. W. N. Transportes Ltda. Considerando o que consta nos autos, em especial a manifestação do Centro de Verificação Veicular (MLFVE) (fl. 05), ratificada pelo Diretor do Departamento de Metrologia Legal e Fiscalização (DMLF) (fl. 05-vº), aliado à manifestação do Diretor de Divisão do Centro de Gestão de Processos (AGGEP) (fls. 06/07-vº), nos quais sugerem a apreensão definitiva do Certificado de Verificação de Veículo-Tanque Rodoviário (fl. 03) em razão da lavratura do Auto de Apreensão 385.291 em face da empresa J. W. N. Transportes Ltda, CNPJ 58.014.564/0001-63 (fl. 02), cujas razões acolho como fundamento e DETERMINO, no desempenho de minhas atribuições legais elencadas no Decreto 55.964/2010, alterado pelo Decreto 64.110/2019 e com fulcro no parágrafo 2º, do artigo 5º do Regulamento Administrativo aprovado pela Resolução Conmetro 8/2006: I. CONVOLAR EM DEFINITIVA a apreensão cautelar do Certificado de Verificação de Veículo-Tanque Rodoviário 1134809, de 2-6-17, pertencente ao veículo-tanque, marca Gotti, placa CZC-3288, em virtude da não conformidade descrita no Auto de Apreensão 385.291, de 13-2-19; II. INVALIDAR o referido certificado, preservando suas informações e integridade, mantendo-o no corpo deste capeado para eventual consulta; III. NOTIFICAR o interessado do teor da presente decisão, via publicação em Diário Oficial do Estado de São Paulo, concedendo- -lhe o prazo de 10 dias para requerer o que entender de direito, nos termos do artigo 20 do Regulamento Administrativo Aprovado pela Resolução Conmetro 8/06; assim, nesse prazo, os autos ficarão disponíveis para vistas, podendo ser requerida no Setor de Atendimento Jurídico, na Sede do Ipem-SP, situada na Rua Santa Cruz, 1.922, térreo, Vila Gumercindo, São Paulo – SP, no horário das 9h às 16h; IV. FIXAR o prazo de 20 (VINTE) DIAS, a contar do término do interregno estabelecido no item antecedente, no caso de não manifestação do interessado, para efetivação das providências enunciadas no item II.</p>"
    };
  },
  methods: {
    getPrice(text) {
      const value = text.length * 0.999;
      return new Intl.NumberFormat("pt-BR", {
        style: "currency",
        minimumFractionDigits: 2,
        currency: "BRL"
      }).format(value);
    },
    getPriceCmPorCol(text) {
      const value = text.length * 0.98;
      return new Intl.NumberFormat("pt-BR", {
        style: "currency",
        minimumFractionDigits: 2,
        currency: "BRL"
      }).format(value);
    },
    openFileDialog() {
      document.getElementById("file-input").click();
    },
    refresh() {
      var storyText = CKEDITOR.instances.editor1.getData();
      var i;
      for (i = 0; i < this.palavras.length; i++) {
        console.log("tes");
        var word = this.palavras[i].text;
        storyText = storyText.replace(
          word,
          '<span id="' +
            this.palavras[i].id +
            '" style="background: red; color:white;padding: 2px; */">' +
            word +
            "</span>"
        );
      }
      this.storyText = storyText;
      this.showWarning = true;
    }
  }
};
</script>
<style>
p > strong {
  font-size: 13px;
}
</style>
