<!DOCTYPE html>
<html lang="en">    

<head>

    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

</head>

<body>

    <script src="https://cdn.botpress.cloud/webchat/v1/inject.js"></script>
    <script src="https://mediafiles.botpress.cloud/a32d4f2c-f5ff-4245-970e-17e762045cf6/webchat/config.js" defer></script>

</body>
    <script>
        window.botpressWebChat.onEvent(
    (event) => {
        if (event.type === 'MESSAGE.RECEIVED') {
        console.log('A new message was received!')
            if(event.value.payload.text === 'You can choose a file'){
                const fileInput = document.createElement('input');
                fileInput.type = 'file';
                fileInput.addEventListener('change', (event) => {
                    const file = event.target.files[0];
                    console.log('Selected file:', file);
                    const reader = new FileReader();
                    reader.onload = async function(event) {
                        const fileContent = event.target.result;
                        const title = file.name;
                        console.log('File content:', fileContent);
                        console.log('File name:', title);
                        window.botpressWebChat.sendPayload({
                            type: 'trigger',
                            payload: {
                                title: title,
                                content: fileContent
                            }
                            })
                        }
                    reader.readAsText(file);
                    });
                fileInput.click();
                

                } 
            }
        
    },
    ['MESSAGE.RECEIVED']
    )

    </script>
</html>
