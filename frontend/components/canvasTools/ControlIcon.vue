<template>
    <div></div>  
</template>

<script>
export default {
    mounted() {
        // Initialise delete icon
        var deleteIcon = "data:image/svg+xml,%3C%3Fxml version='1.0' encoding='utf-8'%3F%3E%3C!DOCTYPE svg PUBLIC '-//W3C//DTD SVG 1.1//EN' 'http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd'%3E%3Csvg version='1.1' id='Ebene_1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' x='0px' y='0px' width='595.275px' height='595.275px' viewBox='200 215 230 470' xml:space='preserve'%3E%3Ccircle style='fill:%23F44336;' cx='299.76' cy='439.067' r='218.516'/%3E%3Cg%3E%3Crect x='267.162' y='307.978' transform='matrix(0.7071 -0.7071 0.7071 0.7071 -222.6202 340.6915)' style='fill:white;' width='65.545' height='262.18'/%3E%3Crect x='266.988' y='308.153' transform='matrix(0.7071 0.7071 -0.7071 0.7071 398.3889 -83.3116)' style='fill:white;' width='65.544' height='262.179'/%3E%3C/g%3E%3C/svg%3E"
        var deleteImg = document.createElement('img')
        deleteImg.src = deleteIcon
        this.$emit('delete-img', deleteImg)

        // Initialise bringToFront icon
        var bringToFrontIcon = "data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHByZXNlcnZlQXNwZWN0UmF0aW89InhNaWRZTWlkIG1lZXQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgc3R5bGU9Ii1tcy10cmFuc2Zvcm06IHJvdGF0ZSgzNjBkZWcpOyAtd2Via2l0LXRyYW5zZm9ybTogcm90YXRlKDM2MGRlZyk7IHRyYW5zZm9ybTogcm90YXRlKDM2MGRlZyk7Ij48cGF0aCBkPSJNMiAyaDl2NEg5VjRINHY1aDJ2MkgyVjJtMjAgMTF2OWgtOXYtNGgydjJoNXYtNWgtMnYtMmg0TTggOGg4djhIOFY4eiIgZmlsbD0iIzYyNjI2MiIvPjxyZWN0IHg9IjAiIHk9IjAiIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgZmlsbD0icmdiYSgwLCAwLCAwLCAwKSIgLz48L3N2Zz4="
        var bringToFrontImg = document.createElement('img')
        bringToFrontImg.src = bringToFrontIcon
        this.$emit('bringToFront-img', bringToFrontImg)

        // Initialise bringForward icon
        var bringForwardIcon = "data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHByZXNlcnZlQXNwZWN0UmF0aW89InhNaWRZTWlkIG1lZXQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgc3R5bGU9Ii1tcy10cmFuc2Zvcm06IHJvdGF0ZSgzNjBkZWcpOyAtd2Via2l0LXRyYW5zZm9ybTogcm90YXRlKDM2MGRlZyk7IHRyYW5zZm9ybTogcm90YXRlKDM2MGRlZyk7Ij48cGF0aCBkPSJNMiAyaDE0djE0SDJWMm0yMCA2djE0SDh2LTRoMnYyaDEwVjEwaC0yVjhoNHoiIGZpbGw9IiM2MjYyNjIiLz48cmVjdCB4PSIwIiB5PSIwIiB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIGZpbGw9InJnYmEoMCwgMCwgMCwgMCkiIC8+PC9zdmc+"
        var bringForwardImg = document.createElement('img')
        bringForwardImg.src = bringForwardIcon
        this.$emit('bringForward-img', bringForwardImg)

        // Initialise sendToBack icon
        var sendToBackIcon = "data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHByZXNlcnZlQXNwZWN0UmF0aW89InhNaWRZTWlkIG1lZXQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgc3R5bGU9Ii1tcy10cmFuc2Zvcm06IHJvdGF0ZSgzNjBkZWcpOyAtd2Via2l0LXRyYW5zZm9ybTogcm90YXRlKDM2MGRlZyk7IHRyYW5zZm9ybTogcm90YXRlKDM2MGRlZyk7Ij48cGF0aCBkPSJNMiAyaDl2OUgyVjJtNyAySDR2NWg1VjRtMTMgOXY5aC05di05aDltLTcgN2g1di01aC01djVtMS0xMnYzaC0zVjhoM20tNSA4SDh2LTNoM3YzeiIgZmlsbD0iIzYyNjI2MiIvPjxyZWN0IHg9IjAiIHk9IjAiIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgZmlsbD0icmdiYSgwLCAwLCAwLCAwKSIgLz48L3N2Zz4="
        var sendToBackImg = document.createElement('img')
        sendToBackImg.src = sendToBackIcon
        this.$emit('sendToBack-img', sendToBackImg)

        // Initialise sendBackwards icon
        var sendBackwardsIcon = "data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHByZXNlcnZlQXNwZWN0UmF0aW89InhNaWRZTWlkIG1lZXQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgc3R5bGU9Ii1tcy10cmFuc2Zvcm06IHJvdGF0ZSgzNjBkZWcpOyAtd2Via2l0LXRyYW5zZm9ybTogcm90YXRlKDM2MGRlZyk7IHRyYW5zZm9ybTogcm90YXRlKDM2MGRlZyk7Ij48cGF0aCBkPSJNMiAyaDE0djE0SDJWMm0yMCA2djE0SDh2LTRoMTBWOGg0TTQgNHYxMGgxMFY0SDR6IiBmaWxsPSIjNjI2MjYyIi8+PHJlY3QgeD0iMCIgeT0iMCIgd2lkdGg9IjI0IiBoZWlnaHQ9IjI0IiBmaWxsPSJyZ2JhKDAsIDAsIDAsIDApIiAvPjwvc3ZnPg=="
        var sendBackwardsImg = document.createElement('img')
        sendBackwardsImg.src = sendBackwardsIcon
        this.$emit('sendBackwards-img', sendBackwardsImg)

        // Initialise pin icon
        var pinIcon = "data:image/svg+xml;base64,PHN2ZyBhcmlhLWhpZGRlbj0idHJ1ZSIgZm9jdXNhYmxlPSJmYWxzZSIgZGF0YS1wcmVmaXg9ImZhcyIgZGF0YS1pY29uPSJsb2NrIiBjbGFzcz0ic3ZnLWlubGluZS0tZmEgZmEtbG9jayBmYS13LTE0IiByb2xlPSJpbWciIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgdmlld0JveD0iMCAwIDQ0OCA1MTIiPjxwYXRoIGZpbGw9ImN1cnJlbnRDb2xvciIgZD0iTTQwMCAyMjRoLTI0di03MkMzNzYgNjguMiAzMDcuOCAwIDIyNCAwUzcyIDY4LjIgNzIgMTUydjcySDQ4Yy0yNi41IDAtNDggMjEuNS00OCA0OHYxOTJjMCAyNi41IDIxLjUgNDggNDggNDhoMzUyYzI2LjUgMCA0OC0yMS41IDQ4LTQ4VjI3MmMwLTI2LjUtMjEuNS00OC00OC00OHptLTEwNCAwSDE1MnYtNzJjMC0zOS43IDMyLjMtNzIgNzItNzJzNzIgMzIuMyA3MiA3MnY3MnoiPjwvcGF0aD48L3N2Zz4="
        var pinImg = document.createElement('img')
        pinImg.src = pinIcon
        this.$emit('pin-img', pinImg)

        // Initialise unPin icon
        var unPinIcon = "data:image/svg+xml;base64,PHN2ZyBhcmlhLWhpZGRlbj0idHJ1ZSIgZm9jdXNhYmxlPSJmYWxzZSIgZGF0YS1wcmVmaXg9ImZhcyIgZGF0YS1pY29uPSJsb2NrLW9wZW4iIGNsYXNzPSJzdmctaW5saW5lLS1mYSBmYS1sb2NrLW9wZW4gZmEtdy0xOCIgcm9sZT0iaW1nIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA1NzYgNTEyIj48cGF0aCBmaWxsPSJjdXJyZW50Q29sb3IiIGQ9Ik00MjMuNSAwQzMzOS41LjMgMjcyIDY5LjUgMjcyIDE1My41VjIyNEg0OGMtMjYuNSAwLTQ4IDIxLjUtNDggNDh2MTkyYzAgMjYuNSAyMS41IDQ4IDQ4IDQ4aDM1MmMyNi41IDAgNDgtMjEuNSA0OC00OFYyNzJjMC0yNi41LTIxLjUtNDgtNDgtNDhoLTQ4di03MS4xYzAtMzkuNiAzMS43LTcyLjUgNzEuMy03Mi45IDQwLS40IDcyLjcgMzIuMSA3Mi43IDcydjgwYzAgMTMuMyAxMC43IDI0IDI0IDI0aDMyYzEzLjMgMCAyNC0xMC43IDI0LTI0di04MEM1NzYgNjggNTA3LjUtLjMgNDIzLjUgMHoiPjwvcGF0aD48L3N2Zz4="
        var unPinImg = document.createElement('img')
        unPinImg.src = unPinIcon
        this.$emit('unPin-img', unPinImg)

        // Initialise edit icon
        var editIcon = "data:image/svg+xml;base64,PHN2ZyBhcmlhLWhpZGRlbj0idHJ1ZSIgZm9jdXNhYmxlPSJmYWxzZSIgZGF0YS1wcmVmaXg9ImZhcyIgZGF0YS1pY29uPSJlZGl0IiBjbGFzcz0ic3ZnLWlubGluZS0tZmEgZmEtZWRpdCBmYS13LTE4IiByb2xlPSJpbWciIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgdmlld0JveD0iMCAwIDU3NiA1MTIiPjxwYXRoIGZpbGw9ImN1cnJlbnRDb2xvciIgZD0iTTQwMi42IDgzLjJsOTAuMiA5MC4yYzMuOCAzLjggMy44IDEwIDAgMTMuOEwyNzQuNCA0MDUuNmwtOTIuOCAxMC4zYy0xMi40IDEuNC0yMi45LTkuMS0yMS41LTIxLjVsMTAuMy05Mi44TDM4OC44IDgzLjJjMy44LTMuOCAxMC0zLjggMTMuOCAwem0xNjItMjIuOWwtNDguOC00OC44Yy0xNS4yLTE1LjItMzkuOS0xNS4yLTU1LjIgMGwtMzUuNCAzNS40Yy0zLjggMy44LTMuOCAxMCAwIDEzLjhsOTAuMiA5MC4yYzMuOCAzLjggMTAgMy44IDEzLjggMGwzNS40LTM1LjRjMTUuMi0xNS4zIDE1LjItNDAgMC01NS4yek0zODQgMzQ2LjJWNDQ4SDY0VjEyOGgyMjkuOGMzLjIgMCA2LjItMS4zIDguNS0zLjVsNDAtNDBjNy42LTcuNiAyLjItMjAuNS04LjUtMjAuNUg0OEMyMS41IDY0IDAgODUuNSAwIDExMnYzNTJjMCAyNi41IDIxLjUgNDggNDggNDhoMzUyYzI2LjUgMCA0OC0yMS41IDQ4LTQ4VjMwNi4yYzAtMTAuNy0xMi45LTE2LTIwLjUtOC41bC00MCA0MGMtMi4yIDIuMy0zLjUgNS4zLTMuNSA4LjV6Ij48L3BhdGg+PC9zdmc+"
        var editImg = document.createElement('img')
        editImg.src = editIcon
        this.$emit('edit-img', editImg)

        //Initialise clone icon
        var cloneIcon = "data:image/svg+xml,%3C%3Fxml version='1.0' encoding='iso-8859-1'%3F%3E%3Csvg version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' viewBox='0 0 55.699 55.699' width='100px' height='100px' xml:space='preserve'%3E%3Cpath style='fill:%23010002;' d='M51.51,18.001c-0.006-0.085-0.022-0.167-0.05-0.248c-0.012-0.034-0.02-0.067-0.035-0.1 c-0.049-0.106-0.109-0.206-0.194-0.291v-0.001l0,0c0,0-0.001-0.001-0.001-0.002L34.161,0.293c-0.086-0.087-0.188-0.148-0.295-0.197 c-0.027-0.013-0.057-0.02-0.086-0.03c-0.086-0.029-0.174-0.048-0.265-0.053C33.494,0.011,33.475,0,33.453,0H22.177 c-3.678,0-6.669,2.992-6.669,6.67v1.674h-4.663c-3.678,0-6.67,2.992-6.67,6.67V49.03c0,3.678,2.992,6.669,6.67,6.669h22.677 c3.677,0,6.669-2.991,6.669-6.669v-1.675h4.664c3.678,0,6.669-2.991,6.669-6.669V18.069C51.524,18.045,51.512,18.025,51.51,18.001z M34.454,3.414l13.655,13.655h-8.985c-2.575,0-4.67-2.095-4.67-4.67V3.414z M38.191,49.029c0,2.574-2.095,4.669-4.669,4.669H10.845 c-2.575,0-4.67-2.095-4.67-4.669V15.014c0-2.575,2.095-4.67,4.67-4.67h5.663h4.614v10.399c0,3.678,2.991,6.669,6.668,6.669h10.4 v18.942L38.191,49.029L38.191,49.029z M36.777,25.412h-8.986c-2.574,0-4.668-2.094-4.668-4.669v-8.985L36.777,25.412z M44.855,45.355h-4.664V26.412c0-0.023-0.012-0.044-0.014-0.067c-0.006-0.085-0.021-0.167-0.049-0.249 c-0.012-0.033-0.021-0.066-0.036-0.1c-0.048-0.105-0.109-0.205-0.194-0.29l0,0l0,0c0-0.001-0.001-0.002-0.001-0.002L22.829,8.637 c-0.087-0.086-0.188-0.147-0.295-0.196c-0.029-0.013-0.058-0.021-0.088-0.031c-0.086-0.03-0.172-0.048-0.263-0.053 c-0.021-0.002-0.04-0.013-0.062-0.013h-4.614V6.67c0-2.575,2.095-4.67,4.669-4.67h10.277v10.4c0,3.678,2.992,6.67,6.67,6.67h10.399 v21.616C49.524,43.26,47.429,45.355,44.855,45.355z'/%3E%3C/svg%3E%0A"
        var cloneImg = document.createElement('img')
        cloneImg.src = cloneIcon
        this.$emit('clone-img', cloneImg)
    },
}
</script>
