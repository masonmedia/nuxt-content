<template>
    <b-container 
    :fluid="fluid" 
    :class="contClass">
        <b-row
        :class="rowClass">
            <slot />
        </b-row>
    </b-container>
</template>

<script>
export default {
    name: 'SectionWrap',
    props: [
        'fluid',
        'contClass',
        'rowClass',
    ]
}
</script>