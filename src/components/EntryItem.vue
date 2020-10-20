<template>
    <div class="entry-item" @click="favoriteEntry(entry.id)">
        <div class="user-profile__entry">
            <div class="entry-item__user">
                @{{ username }}
            </div>
            <div class="entry-item__content">
                {{ entry.content }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "EntryItem",
    props: {
        username: {
            type: String,
            required: true
        },
        entry: {
            type: Object,
            required: true
        }
    },
    methods: {
        favoriteEntry( id ) {
            this.$emit( "favorite", id );
        }
    }
};
</script>

<style>

.entry-item {
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
    box-sizing: border-box;
    cursor: pointer;
    transition: all 0.25s ease;
}

.entry-item:hover {
    transform: scale(1.1, 1.1);
}

.entry-item__user {
    font-weight: bold;
}
</style>