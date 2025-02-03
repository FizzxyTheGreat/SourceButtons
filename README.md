<h1 align="center">Hai aku Fizzxy! <img src="https://user-images.githubusercontent.com/1303154/88677602-1635ba80-d120-11ea-84d8-d263ba5fc3c0.gif" width="40px" alt="Hamlo"><br></h1>

![](https://komarev.com/ghpvc/?username=FizzxyDev&label=PROFILE+VIEWS)
## Using Baileys @fizzxydev/baileys-pro
## NpmJs: [Click Here](https://www.npmjs.com/package/@fizzxydev/baileys-pro)
## Github: [Click Here](https://github.com/FizzxyDev/BaileysV2) 
## Any Question? : [Whatsapp](https://wa.me/6285172200670)


![My Card ](https://cardivo.vercel.app/api?name=FizzxyTheGreat%20&description=”aku%20hanya%20bisa%20memprogram%20nya,%20jika%20kodenya%20sudah%20benar,%20program%20itu%20akan%20berjalan%20sesuai,%20keinginan%20pemilik%20aslinya”%20(%20tapi%20ini%20bukan%20soal%20programnya%20)&image=https://b.top4top.io/p_2090f6xvx0.jpg&backgroundColor=%23ecf0f1&instagram=@wfizzx&github=FizzxyDev&pattern=leaf&colorPattern=%23eaeaea)

___

<p align="center">

  <a href="https://github.com/FizzxyDev"><img title="Author" src="https://img.shields.io/badge/Author-FizzxyDev-red.svg?style=for-the-badge&logo=github" /></a>



</p>
<audio autoplay="true" src="https://f.top4top.io/m_2092qvkoa0.mp3"></audio>

## Shop Message: 
```
client.sendMessage(
    jid, 
    {
        text: "YOUR TEXT",
        title: "YOUR TITLE",
        subtitle: "YOUR SUBTITLE",
        footer: "FOOTER",
        viewOnce: true,
        shop: 3,
        id: "199872865193",
    },
  {
    quoted : m
  }
)
```

## Function Album Message
```
const baileys = require("@fizzxydev/baileys-pro");
async function sendAlbumMessage(jid, medias, options) {
  options = { ...options };

  const caption = options.text || options.caption || "";

  const album = baileys.generateWAMessageFromContent(jid, {
    albumMessage: {
      expectedImageCount: medias.filter(media => media.type === "image").length,
      expectedVideoCount: medias.filter(media => media.type === "video").length,
      ...(options.quoted ? {
        contextInfo: {
          remoteJid: options.quoted.key.remoteJid,
          fromMe: options.quoted.key.fromMe,
          stanzaId: options.quoted.key.id,
          participant: options.quoted.key.participant || options.quoted.key.remoteJid,
          quotedMessage: options.quoted.message
        }
      } : {})
    }
  }, { quoted: m});

  await client.relayMessage(album.key.remoteJid, album.message, {
    messageId: album.key.id
  });

  for (const media of medias) {
    const { type, data } = media;
    const img = await baileys.generateWAMessage(album.key.remoteJid, {
      [type]: data,
      ...(media === medias[0] ? { caption } : {})
    }, {
      upload: client.waUploadToServer
    });
    img.message.messageContextInfo = {
      messageAssociation: {
        associationType: 1,
        parentMessageKey: album.key
      }
    };
    await client.relayMessage(img.key.remoteJid, img.message, {
      messageId: img.key.id
    });
  }

  return album;
}

// How to use ?
sendAlbumMessage(m.chat, [
  { type: "image", data: { url: "https://example.jpg" } },
  { type: "image", data: { url: "https://example.jpg" } }
], { caption: "© FizxxyTheGreat-2025" });
```

## Buttons Message:
```
// send old a buttons
client.sendMessage(m.chat, {
     text: "Hello World !",
     footer: "Fizzxy - 2025",
     buttons: [ 
         { buttonId: `🚀`,
          buttonText: {
              displayText: '🗿'
          }, type: 1 }
     ],
     headerType: 1,
     viewOnce: true
 },{ quoted: null })
 ```
 
## send location buttons:
```
client.sendMessage(m.chat, {
  location: {
    degreesLatitude: -6.2088, // Ganti dengan latitude lokasi
    degreesLongitude: 106.8456, // Ganti dengan longitude lokasi
  },
  caption: "Ini adalah lokasi yang dikirim.",
  footer: "© FizzxyTheGreat",
  buttons: [
          { buttonId: `🚀`,
          buttonText: {
          displayText: '🗿'
          },
           type: 1 }
          ], // isi buttons nya
  headerType: 6,
  viewOnce: true
}, { quoted: m });
```


## send image buttons:
 ```
  client.sendMessage(m.chat, {
  image: { url: "LINK YOUR IMAGE" },
  caption: "Ini pesan gambar Buttons", 
  footer: "© Fizzxy Dev",
  buttons: [
    {
      buttonId: '.owner',
      buttonText: {
        displayText: 'Dev bot'
      },
      type: 1
    },
  ],
  headerType: 1,
  viewOnce: true
}, { quoted: m })
```

## send document buttons:
```
let buttonMessage = {
  document: { url: "https://www.youtube.com/" },
  mimetype: "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
  fileName: "「 FizzxyTheGreat 」",
  fileLength: 999,
  pageCount: 999,
  contextInfo: {
    forwardingScore: 555,
    isForwarded: true,
    externalAdReply: {
      mediaUrl: "https://www.youtube.com/",
      mediaType: 2,
      previewType: "pdf",
      title: "kamu mana punya",
      body: "ini", 
      thumbnail: fs.readFileSync("./path/to/image"),
      sourceUrl: "https://www.youtube.com/",
    },
  },
  caption: "tes",
  footer: "2020",
  buttons: [
    {
    buttonId: "ID MU", 
    buttonText: { 
      displayText: 'Display text' 
    }
  }, {
    buttonId: "ID MU", 
    buttonText: {
      displayText: "DISPLAY TEXT"
    }
  }
  ],
  viewOnce: true,
  headerType: 6,
};

return await client.sendMessage(m.chat, buttonMessage, { quoted: null });
```

## send all buttons interactive:
 ```
const { generateWAMessageFromContent, proto } = require("@FizzxyDev/BaileysPro")
let msg = generateWAMessageFromContent(m.chat, {
  viewOnceMessage: {
    message: {
        "messageContextInfo": {
          "deviceListMetadata": {},
          "deviceListMetadataVersion": 2
        },
        interactiveMessage: proto.Message.InteractiveMessage.create({
          body: proto.Message.InteractiveMessage.Body.create({
            text: "Fizzxy Dev"
          }),
          footer: proto.Message.InteractiveMessage.Footer.create({
            text: "Bot"
          }),
          header: proto.Message.InteractiveMessage.Header.create({
            title: "Igna",
            subtitle: "test",
            hasMediaAttachment: false
          }),
          nativeFlowMessage: proto.Message.InteractiveMessage.NativeFlowMessage.create({
            buttons: [
              {
                "name": "single_select",
                "buttonParamsJson": "{\"title\":\"title\",\"sections\":[{\".menu\":\".play dj webito\",\"highlight_label\":\"label\",\"rows\":[{\"header\":\"header\",\"title\":\"title\",\"description\":\"description\",\"id\":\"id\"},{\"header\":\"header\",\"title\":\"title\",\"description\":\"description\",\"id\":\"id\"}]}]}"
              },
              {
                "name": "cta_reply",
                "buttonParamsJson": "{\"display_text\":\"quick_reply\",\"id\":\"message\"}"
              },
              {
                 "name": "cta_url",
                 "buttonParamsJson": "{\"display_text\":\"url\",\"url\":\"https://www.google.com\",\"merchant_url\":\"https://www.google.com\"}"
              },
              {
                 "name": "cta_call",
                 "buttonParamsJson": "{\"display_text\":\"call\",\"id\":\"message\"}"
              },
              {
                 "name": "cta_copy",
                 "buttonParamsJson": "{\"display_text\":\"copy\",\"id\":\"123456789\",\"copy_code\":\"message\"}"
              },
              {
                 "name": "cta_reminder",
                 "buttonParamsJson": "{\"display_text\":\"Recordatorio\",\"id\":\"message\"}"
              },
              {
                 "name": "cta_cancel_reminder",
                 "buttonParamsJson": "{\"display_text\":\"cta_cancel_reminder\",\"id\":\"message\"}"
              },
              {
                 "name": "address_message",
                 "buttonParamsJson": "{\"display_text\":\"address_message\",\"id\":\"message\"}"
              },
              {
                 "name": "send_location",
                 "buttonParamsJson": ""
              }
           ],
          })
        })
    }
  }
}, {})

return client.relayMessage(msg.key.remoteJid, msg.message, { messageId: msg.key.id })
```

## buttons double:
```
client.sendMessage(m.key.remoteJid, {
  text: "Hello Wolrd !;", 
  footer: "© Fizzxy Dev",
  buttons: [
  {
    buttonId: '.tes',
    buttonText: {
      displayText: 'TESTING BOT'
    },
    type: 1,
  },
  {
    buttonId: ' ',
    buttonText: {
      displayText: 'PRIVATE SCRIPT'
    },
    type: 1,
  },
  {
    buttonId: 'action',
    buttonText: {
      displayText: 'ini pesan interactiveMeta'
    },
    type: 4,
    nativeFlowInfo: {
      name: 'single_select',
      paramsJson: JSON.stringify({
        title: 'message',
        sections: [
          {
            title: 'FizzxyDev - 2025',
            highlight_label: '😜',
            rows: [
              {
                header: 'HEADER',
                title: 'TITLE',
                description: 'DESCRIPTION',
                id: 'YOUR ID',
              },
              {
                header: 'HEADER',
                title: 'TITLE',
                description: 'DESCRIPTION',
                id: 'YOUR ID',
              },
            ],
          },
        ],
      }),
    },
  },
  ],
  headerType: 1,
  viewOnce: true
}, { quoted: m });
```

