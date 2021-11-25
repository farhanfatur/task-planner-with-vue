<template>
    <b-modal size="lg" id="modal-card" ref="formModal" :title="title">
        <div class="row">
            <div class="col-12">
                <label for="title" class="form-label">Title</label>
                <input type="text" class="form-control" v-model="titleTask" placeholder="Title...">
            </div>
        </div>
        <div class="row">
            <div class="col-6">
                <label for="priority" class="form-label">Priority</label>
                <select class="form-control form-select" v-model="priorityTask">
                    <option disabled="disabled" value="">Please Choose Priority</option>
                    <option v-for="(data, index) in priorityList" :key="index" :value="data">{{ data }}</option>
                </select>
            </div>
            <div class="col-6">
                <label for="status" class="form-label">Status</label>
                <select class="form-control form-select" v-model="statusTask">
                    <option disabled="disabled" value="">Please Choose Status</option>
                    <option v-for="(val, index) in statusCards" :key="index" :value="val">{{ val }}</option>
                </select>
            </div>
        </div>
        <div class="row">
            <div class="col-12">
                <label for="note" class="form-label">Note</label>
                <textarea class="form-control" id="note" rows="7" v-model="noteTask" placeholder="Note..."></textarea>
            </div>
        </div>
        <div class="row">
            <div class="col-12">
                <label for="item" class="form-label">Item</label>
                <div class="list-group">
                    <div class="list-group-item list-group-item-action" v-for="(val, index) in newItems" :key="index">
                        <input type="text" class="form-control" :id="val.id" v-model="newItems[index].data" placeholder="Add Item...">
                    </div>
                    <a href="#" class="list-group-item list-group-item-action" @click="addItem">+ Add an Item</a>
                </div>
            </div>
        </div>
        <div class="row" v-show="status != 'addTask'">
            <div class="col-12">
                <label for="comment" class="form-label">Comment</label>
                <textarea class="form-control" id="comment" rows="4" placeholder="Comment..."></textarea>
            </div>
        </div>
        <template #modal-footer>
            <b-button type="button" @click="closeModal">Close</b-button>
            <b-button type="submit" variant="outline-primary" @click="onSubmit">Save changes</b-button>
        </template>
    </b-modal>
</template>
<script>
export default {
    name: "Modal",
    props: {
        statusCards: Array,
        priorityList: Array,
        title: String,
        status: String,
    },
    data() {
        return {
            titleTask: "",
            priorityTask: "",
            statusTask: "",
            noteTask: "",
            newItems: [],
        }
    },
    methods: {
        addItem() {
            let itemId = this.newItems.length
            itemId += 1
            this.newItems = [...this.newItems, {id: itemId, data: ""}]
        },
        closeModal() {
            this.titleTask = ""
            this.priorityTask = ""
            this.statusTask = ""
            this.noteTask = ""
            this.newItems = []
            this.$refs['formModal'].hide()
        },
        onSubmit(e) {
            e.preventDefault()
            let newData = {
                id: Math.floor(Math.random() * 10000),
                title : this.titleTask,
                status : this.statusTask,
                priority : this.priorityTask,
                note : this.noteTask,
                items : this.newItems,
                comments: {
                    count: 0,
                    data: []
                },
                users: {
                    count: 0,
                    data: []
                }
            }
            
            this.$emit('save-card', newData)

            this.titleTask = ""
            this.priorityTask = ""
            this.statusTask = ""
            this.noteTask = ""
            this.newItems = []
            this.$refs['formModal'].hide()
        }
    }
}
</script>