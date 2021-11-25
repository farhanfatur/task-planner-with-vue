<template>
  <div>
    <Header @modalCard="modalCard" />
    <div class="container-fluid">
      <Row :dataTask="dataTask" @showDataCard="showDataCard" />
    </div>
    <Modal :statusCards="statusCards" :title="'Add New Task'" :priorityList="priortyLists" @save-card="saveCard" @close-modal="closeModal" />
  </div>
</template>

<script>
import Row from './components/Row.vue';
import Header from './components/Header.vue';
import Modal from './components/Modal.vue';

export default {
  name: 'App',
  data() {
    return {
      dataTask: [
        {
          id: 1,
          title: "To do List",
          status: "Todo",
          priority: "Low",
          note: "lorem ipsum",
          items: [
            {id: 90, data: "lasjdhkajsd"}
          ],
        },
        {
          id: 2,
          title: "To do List 2",
          status: "Todo",
          priority: "Important",
          note: "lipsumiik",
          items: [
            {id: 91, data: "lorem ipsum"}
          ],
        }
      ],
      statusCards: ["Todo", "Development", "Review", "Done"],
      priortyLists: ["Urgent", "Important", "Medium", "Low"],
      modalView: true,
    }
  },
  components: {
    Row,
    Header,
    Modal
  },
  methods: {
    modalCard() {
      console.log("ok")
    },
    showDataCard(data) {
      if (data.length == 0) {
        data = []
      }
      return data
    },
    closeModal(e) {
      var $self = e
      console.log("Close Modal:", $self.$refs.modalvue)
    },
    saveCard(data) {
      console.log(data)
      this.dataTask = [data, ...this.dataTask]
      
    }
  },
}
</script>

<style>
</style>
