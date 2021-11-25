<template>
    <b-card
        :header="CardTitle"
        header-tag="header"
    >
        <div id="drop-zone-ToDo" @drop="$emit('dropCard', $event, StatusCard)" @dragover.prevent @dragenter.prevent>
            <b-card-body style="padding-left: 0;padding-right: 0;">
                <div id="list-task-ToDo" v-for="(val, index) in Data" :key="index">
                    <div class="card"
                        @click="$emit('showCard', val)"
                        draggable="true"
                        @dragstart="$emit('dragCard', $event, val)"
                        style="cursor: pointer;margin-bottom: 0.5rem"
                        v-b-modal.modal-card
                    >
                        <div class="card-body">
                            <h6 class="card-title">{{ val.title }}</h6>
                            <b-row>
                                <b-col cols="7">
                                    <b-badge :variant="bradeStatus(val.priority)">{{ val.priority }}</b-badge>
                                </b-col>
                                <b-col cols="4">Item: {{val.items.length}}</b-col>
                            </b-row>
                        </div>
                    </div>
                </div>
            </b-card-body>
        </div>
    </b-card>
</template>

<script>
export default {
    name: "CardTask",
    props: {
        CardTitle: {
            type: String
        },
        Data: {
            type: Array
        },
        StatusCard: {
            type: String
        }
    },
    methods: {
        bradeStatus(priority) {
            if (priority == 'Urgent' || priority == 'Important') {
                return "danger"
            }else if(priority == 'Medium') {
                return "warning"
            }else {
                return "success"
            }
        }
    }
} 
</script>